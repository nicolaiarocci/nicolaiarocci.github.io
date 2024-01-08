---
date: 2022-09-08T07:05:25+01:00
title: "The Docker Event Monitor"
description: "How to get alerted when a docker container goes down, or (many) other things happen to it"

share: false
tags: ["til", "open-source", "python", "docker"]
---
I added a new tool to my amateurish DevOps toolbox. Developed in the open by
Tom Williams, the [Docker Event Monitor is][1] a "tiny container that monitors
the local Docker event system in real-time and sends notifications to various
integrations for event types that match the configuration. For example, you can
trigger an alert when a container is stopped, killed, runs out of memory or
health status change." 

At its core sits a simple [python script][2] that monitors the `docker.sock`
file for noticeable changes. The code is straightforward and looks safe to
me. It only took a few minutes to set DEM up so that our `alerts` channel on
Slack gets notified of any health status changes. Some handy options are
included; my favorite is `silence` to set a time window during which alerts are
not fired. It avoids unnecessary spam when routine maintenance goes off on your
stack.

I find [DEM][1] a useful little tool for lightweight, simple deployments where
you're not employing heavy weaponry, like k8s.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://bitbucket.org/quaideman/dem
 [2]: https://bitbucket.org/quaideman/dem/src/master/app/main.py
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
