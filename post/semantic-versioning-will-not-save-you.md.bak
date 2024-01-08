---
date: 2021-03-04T07:05:25+01:00
title: "Semantic Versioning Will Not Save You"
share: false
tags: ["links", "programming"]
---
The always brilliant Hynek recently posted [Semantic Versioning Will Not Save
You][1]. Primarily targeted at *consumers* of SemVer-versioned packages, it is
full of insightful advice.

From my perspective as an open-source maintainer, I can tell you that
versioning is hard. Judging when a new release is going to break backward
compatibility is not as simple as it might seem on the surface, and Hynek does
a great job explaining why. Sometimes it is also hard for me to tell if
a change in a codebase classifies as a new feature, small improvement, or
fix—subtle differences. In the context of SemVer, it matters a lot because
version numbers have a meaning. Consumers will likely decide whether to upgrade
or not based on that meaning.

Admittedly, and precisely because I did not feel comfortable giving guarantees,
the [Eve][1] project has been [0-versioned][3] for seven years. Seven years!
I wanted it to be mature, battle-tested and stable; only then would I feel
comfortable going 1.0. In Eve's case, 1.0 means not only "stable" but also
"done." All major features are in, and they are stable. I am not alone, of
course. Flask, the web-framework on which Eve builds, has been 0-versioned for
many years too. I've also been on the receiving hand of SemVer-related issues,
check the Eve backlog. The same happened with my other projects ([Cerberus][4]
is the exception as it has no dependencies.)

Hynek's point, I think, is that SemVer is a just convention. At each new
release, a semantic-versioned package expresses the maintainer's intention, but
there are no guarantees.

> This does not mean that SemVer is bad or worthless. Knowing the intentions of
> a maintainer can be valuable – especially when things break. Because that’s
> all SemVer is: a TL;DR of the changelog. What it does mean though, is that
> you can’t rely on the semantic meaning of SemVer and **you must treat every
> update as potentially breaking**.

Make sure you read the Taking Responsibility section. It has sound advice on
protecting your project from dependency hell.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://hynek.me/articles/semver-will-not-save-you/
 [2]: https://python-eve.org
 [3]: https://0ver.org/
 [4]: https://python-cerberus.org
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
