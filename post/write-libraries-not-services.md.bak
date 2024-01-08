---
date: 2021-03-25T07:05:25+01:00
title: "Write libraries, not services? Not so fast"
share: false
tags: ["links", "programming", "infrastructure"]
---
[Write libraries instead of services][1] is an interesting article I read
a while ago. I cannot get it off my head. In an attempt to clear up my mind,
I decided to sit down and write about it. I have been writing libraries for
a good part of my life. Most of my earlier dev-work resides on thousands of
computers in the form of libraries. More recently, I have been writing and
deploying remote services. Libraries versus Services is a topic I care about.

Let's jump into the article.

> A service has constant administration costs which are paid by the service
> provider. A properly designed library instead moves these costs to the users
> of the library.

This ignores the issue of support. You are going to have to support your users.
Support comes at a cost. I would argue that, given the distributed nature of
libraries, supporting them can become *very* costly. Your library is probably
residing in a myriad of diverse, local environments. Issues are hard to
replicate or reason about. It is hard to isolate your own code from the
surrounding environment. 

> People say, "services are easy because you can upgrade them centrally, so you
> can avoid slow-to-upgrade users making everyone's lives worse." But this
> assumes that slow-to-upgrade users can have negative effects on everyone
> else. If one user can't have a negative impact on other users, then you don't
> care if some users are slow to upgrade; they're only hurting themselves.

Again, support. Those slow-to-upgrade users are going to not just hurt but
torture your support service with years-old obsolete issues.  If you think it's
the user's responsibility to keep dependencies up to date, good luck with that.
That assumes that developers adopting the library control their deployments,
which isn't often the case. They might employ the library in a desktop
application distributed to dozens (or thousands) of end-users. It could be next
to impossible for them to make sure that all their deployments are up to speed.
Old versions are a pain point and one (if not the most) significant cost
factor. Maintaining a service comes at a cost too, and you'll likely need to
offer some sort of support there as well. A service, however, ensures that all
your users are on the same version, which tremendously reduces the support
effort. 

When weighting costs, support must be factored in, along with all the rest:
development, maintenance, distribution, documentation, etc.  Maybe the
article's author has the luxury of not having to deal with support himself.
Still, there's someone else at his company who has to do that. 

A service, on the other hand, represents a single point of failure. If it goes
down, all users are immediately affected[^2]. By contrast, a nasty bug in your
library will only affect the unlucky users on that version. Now, *this* makes
a significant advantage for distributed libraries.

Your service, however, will talk to all languages via REST, GraphQL, or any
other interface of choice. The library will usually speak just one language.
Yes, you might provide language-specific SDKs for your service, but that's just
an option.

Do you need to hold state? If you do, most of the time, a service will be
a better option. With state comes responsibility, however. You have to
ensure regular backups, resilience, and maintenance, all of them at a cost. 

The author suggests a few approaches to circumventing library limitations. Some
are reasonable, like dynamic linking where it is applicable (not all stacks
support it). Others, quite frankly, I don't understand. 

Many factors influence the choice between service and library, use case and
prevailing circumstances being the main ones. I am not even sure they are
comparable, as they tend to solve different problems. 

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [^2]: I know first hand. We've recently been impacted by a catastrophic event that happened to one of our providers. Our services went down and, with them, a good part of our users. How we overcame the situation and what we learned in the process would probably be worth telling, maybe in a future article.

 [1]: http://catern.com/services.html
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
