---
date: 2022-09-05T07:05:25+01:00
title: "How I stopped Spotify from draining both my RAM and CPU"
share: false
tags: ["spotify", "open-source"]
---
A few days ago, I was browsing my Twitter feed when a [suggestion][2] from my
friend [@flaper87][3] caught my attention:

![](/images/flaper87-on-spotifyd.png)

On my "comfortably old" MacBook Pro[^10], Spotify has been an absolute hog. The
simple act of opening it will require three hundred MBs. That's a remarkable
amount of memory for staying idle and doing nothing useful. Let it play for
a few hours, and have fun glancing at CPU and RAM usage ramping up like there's
no tomorrow. Just for the record, here's Spotify memory usage at launch:

![](/images/spotify-memory-usage.png)


So what exactly is [spotifyd][5]? An open source Spotify client
running as a UNIX daemon.

> Spotifyd streams music just like the official client, but is more lightweight
> and supports more platforms. Spotifyd also supports the Spotify Connect
> protocol, which makes it show up as a device that can be controlled from the
> official clients[^11].

Slow Saturday morning, I decided to give the spotifyd/spotify-tui combo a try.
Setting up spotifyd on a Mac with homebrew is as simple as typing `brew install
spotifyd` and then `brew services start spotifyd` to let it run as a service,
or one can opt to launch it as a stand-alone with `spotifyd --no-daemon`.

As I quickly learned, on a Mac, you need to edit the default configuration file
to update a couple of settings, as reported on the wiki. Namely, I had to set
`backend = 'portaudio'` and `volume_controller = 'softvol'`. While at it,
I also set `use_keyring = true` to avoid storing my Spotify password in the
file. Here's my current configuration settings:


    [global]
    username = "<USERNAME>"
    use_keyring = true

    # On Linux, set both values to 'alsa'
    backend = "portaudio"          
    volume_controller = "softvol"  

    bitrate = 320
    volume_normalisation = true
    normalisation_pregain = -10

    # If set to true, audio data does NOT get cached.
    no_audio_cache = false
    cache_path = "<USER_LIBRARY>/Application Support/Spotify/PersistentCache/Storage"

One minor annoyance that doesn't prevent the server from running as intended
and is only noticeable when I run spotifyd as a stand-alone app is a recurring
and rather obscure "No route to host" warning message. There's an [open
ticket][4] about it. Other than that, spotifyd has been bliss. Most remarkably,
this is the memory usage after a few hours of non-stop streaming:

![](/images/spotifyd-memory-usage.png)

Quite an achievement, considering that we started at 300+ MBs.

I also installed [spotify-tui][6] in an attempt to use it as a replacement for
the official client. As much as I'd love to use it (I love its UI/UX), I can't
say I'm happy with it. It sometimes reports a server disconnect when, in fact,
the underlying spotifyd service is running fine (and I can connect and play
with it from the official client). Secondly, it is sluggish sometimes. Further
investigation revealed that the project is [not actively maintained][1]. For
the time being, I'm connecting to spotifyd from the official iPhone app. I get
the lightweight service with the added benefit that I don't have to switch
windows when I want to interact with Spotify.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://github.com/Rigellute/spotify-tui/issues/1000
 [2]:https://twitter.com/flaper87/status/1564899493572710400
 [3]: https://twitter.com/flaper87
 [4]: https://github.com/Spotifyd/spotifyd/issues/1026
 [5]: https://github.com/Spotifyd/spotifyd
 [6]: https://github.com/Rigellute/spotify-tui
 [^10]: mid-2012. Yes, I know. It's due for replacement later this year, when the M2 MacBook Pro 14" is announced.
 [^11]: Spotifyd requires a Spotify Premium account.
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
