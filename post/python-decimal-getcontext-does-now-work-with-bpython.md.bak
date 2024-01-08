---
date: 2023-06-06T07:05:25+01:00
title: "Python `decimal.getcontext` does not work with bpython"
share: false
tags: ["til", "python", "bpython", "programming"]
---
I have been working on a side project for which I'm using [bpython][1], a "fancy interface to the Python interpreter."
If you use the Python REPL often, you should check it out. It offers unique features like in-line syntax
highlighting, readline-like autocomplete, a "rewind" function to pop the last line of code from memory, auto-indentation
and more.

Anyway, today I found a bug in bpython, and that's that Python's `decimal.getcontext()` does not work with it.

```
bpython version 0.24 on top of Python 3.11.3
>>> import decimal
>>> decimal.getcontext().prec = 6
>>> decimal.Decimal(1) / decimal.Decimal(7)
Decimal('0.1428571428571428571428571429')
```

If you run the same lines in the standard Python REPL, what you get instead is:

```
bpython version 0.24 on top of Python 3.11.3
>>> import decimal
>>> decimal.getcontext().prec = 6
>>> decimal.Decimal(1) / decimal.Decimal(7)
Decimal('0.142857')
```
Further experimenting revealed that, as a workaround, setting `DefaultContext` works as expected:

```
bpython version 0.24 on top of Python 3.11.3
>>> decimal.DefaultContext.prec = 6
>>> decimal.Decimal(1) / decimal.Decimal(7)
Decimal('0.142857')
```

I suspect this has something to do with threads, as `decimal.getcontext` targets the current thread while
`DefaultContext` is global. I went to the bpython repository only to find that a ticket was already opened in 2021. I
[added][2] my `DefaultContext` observation there.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or [follow me on Mastodon][m]*

 [1]: https://bpython-interpreter.org
 [2]: https://github.com/bpython/bpython/issues/918#issuecomment-1578911204
 [rss]: https://nicolaiarocci.com/index.xml
 [m]: https://fosstodon.org/@nicola
 [nl]: https://buttondown.email/nicolaiarocci
