---
date: 2021-03-17T07:05:25+01:00
title: "Battling with SSH, cron jobs, and macOS Keyring"
share: false
tags: ["til", "macos", "cron", "ssh"]
---
So today, I was setting up a cronjob on my trusty MacBook Pro. The goal was to
backup some folders from a remote Linux server via rsync. The script is simple.
It goes something like this:

    rsync -avz -e "ssh -i ~/.ssh/my_rsa_keyfile" myuser@myserver:remotedir/ ~/localdir/

Launched by hand, it works seamlessly. Call it from a cron job via crontab, and
I get a permission denied error. I then enabled ssh `-v` option to gather
a little intel on what was actually going on. As it turns out, the exact
error was: 

    `read_passphrase: can't open /dev/tty: Device not configured`

Quite puzzling. Long story short, the error message was misleading. It took me
an embarrassingly long time to figure out what the real problem was. The
identity file I was using has a passphrase, which is saved in macOS Keyring.
When the `ssh -i` command is launched via cron, no Keyring is used. Not unless
you explicitly instruct ssh to do. See, my `~/.ssh/config` file was something
like this:

    Host *
        ServerAliveInterval 360
        AddKeysToAgent yes

    [...]

    Host myserver
        HostName 123.123.123.123
        User myuser

See, in `myserver` section there was no `Usekeychain` option. Launching the
script interactively worked because of `AddkeysToAgent` in the general section.
It enables the ssh-agent for the current terminal session, for all hosts. But
cron jobs, well, they don't run in the same session, and certainly don't run
the agent. I could eval the agent in the script, of course, but the
simplest solution was to update `myserver` section:

    Host myserver
        HostName 123.123.123.123
        Usekeychain yes
        User myuser

Now ssh knows it should use the keychain when resolving `myserver` RSA key,
even when no agent is running. I am not sure why I did not have `Usekeychain`
there; I do have it enabled for other hosts in the same file. As said, I wasted
way too much time on this issue. At least, I hope my experience will be useful
to someone else, or, more likely, to my future self in a few months or years.


*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
