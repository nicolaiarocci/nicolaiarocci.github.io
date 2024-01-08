---
date: 2021-08-25T07:05:25+01:00
title: "How to restore a single Postgres database from a pg_dumpall dump"
share: false
tags: ["til", "postgres"]
---
Today I learned how to restore a single Postgres database from a global dump
generated with [`pg_dumpall`][1]. Now, `pg_dumpall` is handy when you want to back
up an entire Postgres cluster. It will dump all databases and global objects in
a single text file. In contrast, [`pg_dump`][2], the go-to tool for Postgres
backups, offers more control but only works with a single database and doesn't
dump global objects, such as the roles/users linked to the database.

The problem with `pg_dumpall` comes when you want to restore just one database
from the dump file. That's not supported out of the box, but it is achievable
with some tinkering. 

The `pg_dumpall` dump is a plain text file that contains all the SQL commands
needed to restore the cluster. All database instructions are there as well; we
only need to extract them. Say we have one "mydb" database that we need to
retrieve. Open the dump file and look for a string starting with "connect
mydb". That's where our database instructions begin. Then look for the first
occurrence of "PostgreSQL database dump complete". That's where the
instructions end. [This][3] script, which I have to say makes clever use of `sed`,
will do just that for us:

    #!/bin/bash
    [ $# -lt 2 ] && { echo "Usage: $0 <postgresql dump> <dbname>"; exit 1; }
    sed  "/connect.*$2/,\$!d" $1 | sed "/PostgreSQL database dump complete/,\$d"

The output will be to STDOUT; we want to pipe it into a file. If we named the
script `pg_extract.sh`, as I did, we'd do:

    ./pg_extract.sh dumpall.sql mydb >> mydb.dump

Now we have the specific DB dump, and we can restore it like this:

    psql (connection options) mydb < mydb.dump

If the database still exists on the cluster, we first want to drop it, or we'll
only get error messages:

    psql (connection options) -d postgres -c "DROP DATABASE IF EXISTS mydb"
    psql (connection options) -d postgres -c "CREATE DATABASE mydb"

`DROP DATABASE` will fail if there are active connections. Either
[force-drop][4] all active connections or tell your peers to leave the database
alone. Merging the above passages in a script is an option.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://www.postgresql.org/docs/current/app-pg-dumpall.html
 [2]: https://www.postgresql.org/docs/current/app-pgdump.html
 [3]: https://stackoverflow.com/a/48866503/323269
 [4]: https://stackoverflow.com/a/5408501/323269
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
