---
date: 2022-01-16T07:05:25+01:00
title: "Automatic deletion of older records in Postgres"
share: false
tags: ["til", "postgres"]
---
We have a Postgres cluster with a database for each user. Each database has
a table that records events, and we want this table to only record the last 15
days.

If we were on MongoDB, we could use a [capped collection][1], but we are in
Postgres, which does not have equivalent functionality. In Postgres, you have
to make do with something homemade. My first idea was to install a cron job in
the system. It would execute daily, deleting older events in each user
database. 

Before jumping in, I looked at what others do. One surprising popular approach
appears to be using [triggers][2]: older ones are pruned when a new row is
inserted in the table. For my use case, this seems unnecessarily taxing to the
system. I'm happy with running a single maintenance task late in the night when
the system is underused. Two other solutions are [pgAgent][3] or [pg_cron][4].
pgAgent is an external UI tool, so hard No to pgAgent from me. pg_cron
essentially offers cron jobs baked into the database, which is good, but, like
pg_Agent, it requires you to install the tool itself, create a Postgres
extension, change Postgres configuration, optionally grant usage to a schema,
etc. There's also [partitioning][5], which seems way overboard for our use
case. It seems that these approaches demand new dependencies and unnecessary
work for something I can easily accomplish by leveraging what is already
available, for free, in the system. So, it's good old Linux cron jobs for me.

Because we run Postgres in Docker, a little more work is involved, but overall,
the solution is pretty straightforward. Here is the script I came up with:

    readonly CONTAINER=$(docker ps -q -f name=postgres)
    readonly USER=dbuser
    docker exec -i $CONTAINER \
        psql -U $USER -d postgres -t \
            -c "select datname from pg_database where datname like 'cus_%'" | \
        xargs -n 1 -I"{}" docker exec -i $CONTAINER psql -U $USER -d {} -t \
            -c "delete from mytable where datetime < now() - interval '15 days'"


First, we find the id of the docker container (it runs in a swarm, so we don't
have exact container names). We need it because we want to execute psql from
within the container. The second row sets a Postgres user other than the
default one. That's because we don't allow default user logins. Then comes the
Linux pipeline. First, we execute a query that returns all user database names;
then, we pipe those into the query that deletes obsolete rows. The query
executes against each target database. The script is then installed as a cron
job with something similar to:

    0 4 * * * /home/user/dir/cleanup.sh

Which ensures the script runs daily at 4 am. For a weekend task, I'm happy with
the result.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://docs.mongodb.com/manual/core/capped-collections/
 [2]: https://www.postgresql.org/docs/current/sql-createtrigger.html
 [3]: https://www.pgadmin.org/docs/pgadmin4/latest/pgagent.html
 [4]: https://github.com/citusdata/pg_cron
 [5]: https://www.postgresql.org/docs/current/ddl-partitioning.html
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
