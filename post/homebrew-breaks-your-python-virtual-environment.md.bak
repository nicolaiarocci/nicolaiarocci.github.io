---
date: 2021-02-08T07:05:25+01:00
title: "When Homebrew breaks your Python virtual environment"
share: false
tags: ["python", "programming", "links"]
---
Ever had your old, trusty Python virtual environment fail on you? I sure did.
Sometimes, when I activate or switch between virtual environments, I get the
following error:

    $ workon eve
    dyld: Library not loaded: @executable_path/../.Python

I never really took the time to look into it. When this happens, because I am
in a rush (and because I am a lazy old fart), I shrug it off, recreate the
virtual environment on the spot, and get back to work. 

My friend Justin Mayer knows better. The other day, he posted a [short
insightful article][1] about this very same issue:

> Perhaps you heard stories about why you shouldn’t use the system-bundled
> Python, so instead you use Homebrew to install Python and then use its
> interpreter to create a virtual environment. A month later, you activate that
> same environment, and when you try to use it, you see this inscrutable error:
> (...) What happened? The Python interpreter referenced by the virtual
> environment… no longer exists. But how can that be? You didn’t change
> anything! You didn’t change anything… but Homebrew did.

Homebrew is the culprit. If you have been affected (and if you have done any
length of serious Python work, you have), then go [read][1] Justin's piece. He
explains the whys and then goes into the hows you solve the problem for good.


*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://justinmayer.com/posts/homebrew-python-is-not-for-you/
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
