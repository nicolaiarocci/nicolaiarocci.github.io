---
date: 2021-02-23T07:05:25+01:00
title: "Musings on Python's Pattern Matching"
share: false
tags: ["python", "programming"]
---
Pattern Matching [is coming][1] to Python, and I am not sure I like it. Don't get me
wrong, I love pattern matching. I use it all the time in F#. I am sure that
once it lands in the language, it will be wildly adopted. 

So what's the problem with Python's pattern matching? The community, some core
developers included, has expressed [several concerns][2]. The Python Steering
Council has acknowledged them and is willing to look into improvements should
they be proposed. I am not going into the details here. You can look them up
yourself. Let's just say that there are a few gotchas, like the requirement to
use dotted names as constants, to prevent them from being interpreted as
capture variables instead (doh!) The lack of local scope bites hard here.

If we look at pattern matching in isolation, it is undoubtedly desirable. There
ought to be a reason why every language on the planet is trying to adopt it. Is
it pythonic? I doubt it. With all its corner cases and the odd syntax, I think
that the current design adds quite a bit of complexity to the language. As
someone [noted][6], core dev Larry Hastings puts it well:

> I dislike the syntax and semantics expressed in PEP 634. I see the match
> statement as a DSL contrived to look like Python and to be used inside of
> Python, but with very different semantics. When you enter a PEP 634 match
> statement, the rules of the language change completely, and code that looks
> like existing Python code does something surprisingly very different ([source][3])

I especially agree with this sentiment, and I am still quoting Hastings:

> **I think the bar for adding new syntax to Python at this point in its life
> should be set very high**. The language is already conceptually pretty large,
> and every new feature means new concepts one must learn if one is to read an
> arbitrary blob of someone else's Python code. The bigger the new syntax, the
> higher the bar should become, and so the bigger payoff the new syntax has to
> provide.

Unfortunately, I feel like this trend of getting away from pythonic-Python has
been going on for a while. As my friend Alessandro Molina mentioned just today:

> I have been thinking about how Python has been moving away from its own Zen
> since the time of "async" keyword. Convenience rarely values added
> complexity. Never been a big fan of adding keywords that will be misused by
> the majority to deal with the vertical needs of a minority ([source][4])

He was referring to group exceptions, not pattern matching. Still, his tweet
struck a nerve as I was busy writing down these thoughts.  

More generally, I am concerned with all the recent attempts to take features
from functional languages and bring them over to object-oriented languages.
It's not just a Python thing; C# just ported Records, pattern matching, and
a few other things over from F#/ML. I understand that like 85% of the software
development crowd is into object-oriented languages, but look, it's going to
exceptionally hard to successfully and seamlessly move features from apples to
oranges.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://lwn.net/Articles/845480/
 [2]: https://discuss.python.org/t/gauging-sentiment-on-pattern-matching/5770
 [3]: https://discuss.python.org/t/gauging-sentiment-on-pattern-matching/5770/21
 [4]: https://twitter.com/__amol__/status/1364205630928617473
 [5]: https://github.com/gvanrossum/patma/blob/master/README.md
 [6]: https://news.ycombinator.com/item?id=26083779
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
