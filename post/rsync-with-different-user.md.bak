---
date: 2023-08-23T07:05:25+01:00
title: "rsync with a different user"
share: false
tags: ["til", "rsync", "bash", "linux"]
---
Today I learned how to rsync with a user different than the one connected to the remote. Why would one want to do such a
thing? The data I need to download from that server is owned by 'backup,' a different, service-only user. I wanted to
avoid going the change-permissions slippery route and allow my user direct access to the data.

Looking at the rsync documentation, I learned about the nifty `--rsync-path=PROGRAM` [option][1]:

> Use this to specify what program is to be run on the remote machine to start-up rsync. Often used when rsync is not in
> the default remote-shell's path (e.g. --rsync-path=/usr/local/bin/rsync).

The example caught my attention. I could perhaps leverage this option to perform a user switch before executing rsync
(now performed on the remote machine). As further research confirmed, it [can be done][2]:

```
rsync --rsync-path 'sudo -u backup rsync' -a --delete host:source destination
```

It didn't work immediately because my user was not a sudoer, but that was an easy fix:

```
cat > /etc/sudoers.d/myuser << EOF
myuser ALL=(ALL) NOPASSWD:/usr/bin/rsync
EOF
```

As you can see, not only must the user be a sudoer, but it also needs to be able to sudo with no password. One last
minor issue was that 'backup', being a service user, had no shell access. That was another easy fix:

```
sudo usermod -s /bin/bash backup
```

Now my rsync-with-a-different-user command works like a charm. I do have some mild security concerns, though. My user is
a sudoer (can only sudo rsync, though[^3]), and 'backup' now has shell access. As password logins are turned off, and
SSH keys-only access is allowed to the machine (and I'm the only person holding those keys), everything's still
reasonably safe. Are there better ways? Please let me know. 

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or [follow me on Mastodon][m]*

[1]: https://download.samba.org/pub/rsync/rsync.1#opt--rsync-path
[2]: https://unix.stackexchange.com/a/546296
[^3]: Thanks to Sebastian on Mastodon for [pointing out](https://fosstodon.org/@DarkMetatron@rollenspiel.social/110939139075153024) that I should limit the sudoer to just rsync itself. I updated the post accordingly. By the way, this is why I love posting TILs in public.
 [rss]: https://nicolaiarocci.com/index.xml
 [m]: https://fosstodon.org/@nicola
 [nl]: https://buttondown.email/nicolaiarocci
