---
title: Open Source and Code Responsibility
author: Nicola Iarocci
date: 2014-10-21
url: /open-source-and-code-responsibility/
dsq_thread_id:
  - 3139339064
categories:
  - Programming
tags:
  - eve
  - open source
  - python
---
Last week I was speaking at an Open Source panel at [Better Software 2014][1], and one of the topics that we touched was code responsibility. This is an important topic for anyone who is maintaining an open source project, especially when it comes to the process of reviewing and accepting code contributions.

At some point during the debate, I argued that when a maintainer merges a pull request, he (or she) implicitly agrees on being responsible for that code. That seemed to strike some surprise into most attendees.

Yes, in theory any contributor is just a ping away so in case trouble arises one can always reach him, or her. Unfortunately this is not always the case. While some contributors will fully embrace your project and keep helping after their initial contribution, truth is that a good number of them will just move on, never to be seen again.

There&#8217;s nothing wrong with that. Not everyone has spare time to devote to your project, which is perfectly fine. It is natural for most people to contribute what they need to a project and then go on their way. Actually, one could argue that most projects grow and prosper precisely thanks to this kind of contributions.

However this attitude can become an incumbent when big chunks of code get merged, usually as new (big) features. Good practices advice against merging huge pull requests. In fact they are rare and when they do come, it is a good idea to ask for them to be split into smaller ones. But no matter the format, a huge contribution is likely to hit a project one day or another. It might even come from more than one person: a disconnected and distributed team of contributors who have been patiently tinkering on a side branch or a fork for example. When this happens, and provided that the contribution is worth merging, the maintainer should then ask him/herself the obvious question: _am I willing to deal with the consequences of this merge?_ <!--more-->

In fact this is the exact scenario I&#8217;m dealing with right now. The [Eve][2] project has always been a MongoDB shop. Since its inception however people have been asking if (when) SQL support was going to be added. I think we were in Alpha when someone started contributing SQL code. Over time I ended up devoting a specific branch to this feature. Several people have been hacking at it since then, and what a splendid job they did! To say that it was a huge commitment is an understatement but, in time, they managed to deliver. So now we have this awesome [sqlalchemy branch][3] which is feature complete and ready to be merged ahead of the new Eve release. We&#8217;re talking 4K+ lines of code and 44 files changed. Code quality is not under discussion. I know that several companies and individuals have been using that branch in production with good success, even when it still was at its early stages.

This is very exciting as adding SQL support has a good chance to greatly improve the audience of the project. At the same time however, I&#8217;m a little bit nervous if not scared, and I have been for a while. Am I ready to deal with the consequences of this supermerge? Inevitably SQLAlchemy tickets will be opened and Stack Overflow questions will be asked. SQL-related pull requests will come in and mailing list posts will flock. To be honest I don&#8217;t think I can handle that, let alone allocate more of my free time to the project. Also, I&#8217;m not very confident with SQLAlchemy itself so I would not be the best person deal with that code anyway. In the recent past while discussing SQLAlchemy support on the mailing list, I have been [very clear about my concerns][4], so much that I probably scared a few people away. What worries me the most, I suspect, is the risk of new code becoming stale one day or another. In time that would probably impact the reputation of the whole project.

To think about it, we already had something similar happen in the past, although for a smaller feature. The [Document Versioning][5] pull request, contributed by the amazing [Josh Villbrandt][6], had been daunting me with similar thoughts. New code was going to be be quite intrusive, adding a good deal of complexity to an otherwise relatively simple codebase. Everything went amazingly well though. Josh is still an active contributor. He helps with improving his own feature and, even more importantly, other contributors are now helping with Document Versioning [as we speak][7]. Overall, the Eve project as a whole as been enjoying a growing number of skilled contributors and adopters. It&#8217;s been a joy to see people commenting on open tickets, offer support on the mailing list and even on Stack Overflow. So that should be encouraging.

So here I sit, with 4K LOCs ready to be merged. What do I do with them? I considered a few options. One is leaving the SQL feature in a separate branch. Another is to ask the team to refactor the whole thing into an external extension (we have [a few][8] already). By doing any of these Eve-core would remain MongoDB only and I could keep managing it on my own. But then again, none of these options would add native SQL support to Eve. Also, an extension or a branch would run even a greater danger of becoming stale.

At some point I guess even mildly successful projects like Eve have to decide wether they want to outgrow their author. I strongly believe that growing and trusting communities is all that open source is about. You release your work out there and, even at that early stage, you are already entrusting people. You trust that they will take notice and then that they will validate your project (or not). Eventually, someone will review your code, adopt it and, in time, contribute. The project then grows up to a point where its community becomes so predominant that you, as the author and maintainer, just have to let some control go.

So yes, SQL support is coming to Eve, and as a native feature. I trust that the contributors to the SQLAlchemy backend will stay around and, if they won&#8217;t, that someone else will stand up and take the torch. I am also confident that the community as a whole will adopt the feature, make it grow and well&#8230; we&#8217;ll see what happens next.

If you want to get in touch, I&#8217;m [@nicolaiarocci][9] on Twitter.

 [1]: http://www.bettersoftware.it
 [2]: http://python-eve.org
 [3]: https://github.com/nicolaiarocci/eve/tree/sqlalchemy
 [4]: https://groups.google.com/forum/?hl=en#!topic/python-eve/11t1usVH2EY
 [5]: http://python-eve.org/extensions
 [6]: https://github.com/joshvillbrandt
 [7]: https://github.com/nicolaiarocci/eve/pull/486
 [8]: http://python-eve.org/features.html#document-versioning
 [9]: https://twitter.com/nicolaiarocci
