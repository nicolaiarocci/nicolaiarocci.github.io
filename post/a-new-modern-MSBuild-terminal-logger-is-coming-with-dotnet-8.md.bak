---
date: 2023-05-20T07:05:25+01:00
title: "A new modern MSBuild terminal logger is coming with .NET 8"
slug: a-new-modern-msbuild-terminal-logger-is-coming-with-dotnet-8
share: false
tags: ["dotnet", "programming"]
---
The [latest .NET 8 Preview][1] is out, and I love that they're finally changing how MSBuild logs are printed to the terminal.
The new Terminal Logger ditches the infamous "wall of text" that is a nightmare to parse in favor of a cleaner, leaner,
and more organized output.

> Once enabled, the new logger shows you the restore phase, followed by the build phase. During each phase, the
> currently-building projects are at the bottom of the terminal, and each building project tells you both the MSBuild
> Target currently being built, as well as the amount of time spent on that target.

The new MSBuild terminal logger is not the default. It must be opted-in with the `tl` option of the `dotnet build`
command. Here's what it looks like for a complex, multi-project and multi-target solution:

![MSBuild Terminal Logger output](/images/modernbuildoutput.gif)

Now, if you're doing .NET programming within an IDE like Rider of Visual Studio, this all might seem of little
importance to you, but rest assured as soon as you have to look at CI logs or if you use the command line in your
workflow a lot as I do, this is pure bliss. 

Interestingly, this marks only the first step in a series of upcoming MSBuild UX improvements: *"We hope to use this
logger as the foundation for a new batch of UX improvements for MSBuild, including aspects like progress reporting and
structured errors in the future."* Color me excited.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or [follow me on Mastodon][m]*

[1]: https://devblogs.microsoft.com/dotnet/announcing-dotnet-8-preview-4/

 [rss]: https://nicolaiarocci.com/index.xml
 [m]: https://fosstodon.org/@nicola
 [nl]: https://buttondown.email/nicolaiarocci
