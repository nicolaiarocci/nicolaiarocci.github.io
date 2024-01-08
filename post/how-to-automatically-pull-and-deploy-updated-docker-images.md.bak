---
date: 2021-11-21T07:05:25+01:00
title: "How to automatically pull and deploy updated Docker images"
share: false
tags: ["til", "docker"]
---
We want our test and production stacks to be automatically updated every time
something new is pushed to the `test` or `release` branch. CI builds the docker
image on successful test runs, then stores it in our private registry. But how
do you automatically pull and deploy those updated images?

I looked into the [Watchtower][1] project, which is interesting. You add
Watchtower to the stack, and it will diligently check for new versions of the
images used by the containers in the stack, pulling, building and deploying as
needed while the stack is up and running. In my experiments, however, I had
[little luck][2] in making it talk with our private registry. Also, I'm not too
fond of polluting my stack with foreign containers. I want my docker stack to
be simple, tidy, clean, and single-tasked. 

I ended up doing something super simple. A cronjob routinely invokes a script
that pulls relevant images from our registry. If updated images are downloaded,
then the `docker stack up` command is issued.  Finally, a `docker image prune
-af` ensures obsolete images are deleted. For the simplest scenario, where we
only need to take care of one image, the script looks like this:

    #!/bin/bash
    set -e

    readonly IMAGE=[image]
    readonly TAG=[tag]

    out=$(docker pull $IMAGE:$TAG)

    if [[ $out != *"up to date"* ]]; then
        echo "an updated image has been donwloaded for '$IMAGE:$TAG'"
        # we actually launch a script here:
        docker stack up -c stack.yml mystack --with-registry-auth
        docker image prune -af
    else
        echo "no updates available for '$IMAGE:$TAG'"
    fi

I expected `docker pull` to return `1` on successful pulls; it turns out it
always returns `0`, so I'm checking its output for confirmation (I got the hint
[here][3]).

You might be wondering why we don't directly execute `docker stack up` in our
cronjob. It updates the stack resolving new images by default. The problem is
that, in our experience, it also briefly stops the services. Not an issue if
you run this command sporadically. We want our stacks refreshed minutes after
the initial developer push, though, so the cronjob runs frequently. With our
pre-fetch approach, actual deployment only happens when an updated image has
been found and downloaded.

Now, when I push to, say, `test` branch, I have the updated services up and
running a minute later, without me doing anything on the docker or server-side
of things. Mission accomplished, I guess, but I am sure there are other, better
ways around this problem. If you happen to know one, please let me know about
it (keep in mind, we don't use alternative orchestrators, just the built-in
'swarm' thing.)

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://containrrr.dev/watchtower/
 [2]: https://github.com/containrrr/watchtower/issues/1113
 [3]: https://stackoverflow.com/a/51628017/323269
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
