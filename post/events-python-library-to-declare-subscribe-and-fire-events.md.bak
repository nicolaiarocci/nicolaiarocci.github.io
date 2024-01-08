---
date: 2020-08-17T07:05:25+02:00
title: "Events and callbacks in the Python language"
share: false
---

So last week I got an email from my friend Michael Kennedy. Michael runs the
[TalkPython Training][1] website, arguably the best place where you can learn
Python today. He also hosts two popular Python podcasts: [TalkPython][7] and
[PythonBytes][8], the latter co-hosted with Brian Okken. He is super active in
the Python space, so much that he received the Python Software Foundation
Fellow Membership back in 2018. I first met Michael back in 2014, I think, at
MongoDB Headquarters in New York, where we were both invited as part of the
MongoDB Masters program. We shared a C#/.NET background, which was something of
note in that context, and I remember Michael being curious about me embracing
Python and my first open-source release in that space. Fun times.

Anyways, back to his email. He mentioned my little [Events][2] library and told
me that they covered it in [episode #194][3] of the PythonBytes podcast. I was
delighted, of course, and a little surprised too, as Events has been out for
several years. Like its bigger brother [Cerberus][4], I built Events as I was
working on the [Eve][5] project. Unlike Cerberus, which got a lot of traction
on its own (outside of the Eve eco-system), Events did not get a lot of
attention. Not as a stand-alone at least. People are leveraging its features
every time they use [event hooks][9] in Eve, but, albeit mentioned in the
documentation, few realize that they can add support for dynamic
callbacks directly to their projects.

Michael mentioning Events in the podcast was gratifying. He also published
a gist with a [concrete usage example][6], and then he went ahead and submitted
a pull request with some documentation improvements, with some more PRs to come
in the future.

But what exactly is Events? The C# language provides a handy way to declare,
subscribe to, and fire events. Technically, an event is a "slot" where callback
functions (event handlers) can be attached to - a process referred to as
"subscribing to an event." Events is a little handy package that encapsulates
the core to C# event subscription and firing, to make it feel like a natural
part of the Python language. Not surprisingly, Events is dubbed *Python Event
Handling, the C# Style.*


```
>>> def something_changed(reason):
...     print "something changed because %s" % reason
...

>>> from events import Events
>>> events = Events()
>>> events.on_change += something_changed
```

Multiple callback functions can subscribe to the same event. When the event
fires, all attached event handlers are invoked in sequence. To fire the event,
perform a call on the slot:


```
>>> events.on_change('it had to happen')
'something changed because it had to happen'
```

Intrigued? I sure hope so. Check out the [Events repository][2] on GitHub.


*Enjoyed this post? Subscribe to the [newsletter][nl] or follow @[nicolaiarocci][tw] on Twitter.*

 [1]: https://training.talkpython.fm/
 [2]: https://github.com/pyeve/events/
 [3]: https://pythonbytes.fm/episodes/show/194/events-and-callbacks-in-the-python-language
 [4]: https://github.com/pyeve/cerberus/
 [5]: https://github.com/pyeve/eve/
 [6]: https://gist.github.com/mikeckennedy/7235543fd5964bebabe1e3546ce67d91
 [7]: https://talkpython.fm/
 [8]: https://pythonbytes.fm/
 [9]: https://docs.python-eve.org/en/stable/features.html#eventhooks
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: http://eepurl.com/b-_Pzz

