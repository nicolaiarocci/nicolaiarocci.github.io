---
date: 2021-05-25T08:05:25+01:00
title: "So tired of Homebrew messing up with my stuff"
share: false
tags: ["homebrew", "macOS"]
---
Pardon me while I'm venting out my frustration. I am so tired of Homebrew
messing up with my stuff. It used to be the perfect tool for the right job
until they decided to auto-brew-update-and-cleanup at every new install.
Another day another issue, today with vim not running anymore:

    dyld: Library not loaded: /usr/local/opt/lua/lib/liblua.5.3.dylib
    Referenced from: /user/local/bin/vi
    Reason: image not found

Lua has suddenly gone missing. Ah, but of course. I installed something with
Homebrew this morning. The fix is to `brew reinstall vim`, which then leads to
the following error:

    Error: python@3.9 the bottle needs the Apple Command LIne Tools to be installed.
    You can install them, if desired, with:
    xcode-select --install

An `xcode-select install` and another `brew reinstall` later, vim is back home.
It's only a minor annoyance —only a few wasted minutes, but the point is, they
didn't need to be wasted. If you're frequently installing stuff via Homebrew,
this is quite a common, unpleasant occurrence (python virtual environments
being hit with alarming frequency).

I know that one can disable automatic cleanups by setting the
`HOMEBREW_NO_INSTALL_CLEANUP` environment variable. I will end up doing that
out of frustration sooner or later. Again, the point is I should not need to do
that.  It all adds unnecessary friction, especially for someone who's been
religiously running manual cleanups (I concede that an un-maintained brew cache
can grow to *very* sizable dimensions).

Homebrew is still an essential tool; just not so enjoyable anymore. It's not
like we have a valid alternative at hand, anyway.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
