---
date: 2023-06-20T07:05:25+01:00
title: "Homebrew and docfx don't like each other too"
share: false
tags: ["dotnet", "docfx", "homebrew", "programming"]
---
Another day another Homebrew incompatibility emerges, this time with [docfx][2], the technical documentation building
tool of reference in .NET space. I've been using docfx for years to build the [FatturaElettronica.NET][3] website, and it's
always been working without a glitch. Lately, however, my builds have been failing with strange errors I was too lazy to
diagnose until today when I decided to grasp the nettle and sort the whole thing out.

It took me an embarrassing time to realize that, while successful, my docfx updates (`dotnet tool update -g docfx`) were
being ignored. An old, Homebrew-installed version of docfx was being executed at my launches —a simple `which docfx`
revealed the issue. `brew uninstall docfx` finally set the updated, dotnet-installed version free of its chains, and it
is now merrily churning websites.

A similar issue emerged [between Homebrew and .NET 8 Preview][1] only a few days ago. Lesson learned I'm not installing
dotnet tools via Homebrew anymore. Or maybe, I might stay clear of Homebrew altogether.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or [follow me on Mastodon][m]*

[1]: /homebrew-and-dotnet-8-preview-dont-like-each-other/
[2]: https://dotnet.github.io/docfx/index.html
[3]: https://fatturaelettronicaopensource.org
 [rss]: https://nicolaiarocci.com/index.xml
 [m]: https://fosstodon.org/@nicola
 [nl]: https://buttondown.email/nicolaiarocci
