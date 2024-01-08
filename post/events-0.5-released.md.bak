---
date: 2023-07-31T07:05:25+01:00
title: "Events 0.5 released"
share: false
tags: ["open-source", "python", "events"]
---
Today I released [Events 0.5](https://pypi.org/project/Events/0.5/). Thanks to [Cailean
Parker](https://github.com/CaileanMParker)'s contribution, we added support for the `__getitem__` dunder (aka Python
magic method.) This allows the calling of events from strings, thus enabling dynamic events. For instance:

```
events = Events(tuple(f"on_{i}" for i in range(5)))

for i in range(5):
    events[f"on_{i}"](i)
```

The C# language provides a handy way to declare, subscribe to and fire events. In C#, an event is a "slot" to which
callback functions (event handlers) can be attached - a process referred to as subscribing to an event. *Events* adds
this mechanism to Python. It originated as a side experiment (I was a C# transfugee then) that I later adopted as an
[Eve](https://github.com/pyeve/eve) dependency. It slowly got some traction besides my projects. Read more on the project's [GitHub
page](https://github.com/pyeve/events).

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or [follow me on Mastodon][m]*

 [rss]: https://nicolaiarocci.com/index.xml
 [m]: https://fosstodon.org/@nicola
 [nl]: https://buttondown.email/nicolaiarocci
