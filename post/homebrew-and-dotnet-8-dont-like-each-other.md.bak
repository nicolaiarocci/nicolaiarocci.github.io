---
date: 2023-06-13T07:05:25+01:00
title: "Homebrew and .NET 8 Preview don't like each other"
slug: homebrew-and-dotnet-8-preview-dont-like-each-other
share: false
tags: ["til", "dotnet", "programming", "homebrew", "csharp"]
---
Today I learned that .NET 8 Preview could play better with Homebrew (or vice-versa). I'm working on a [C# 12 presentation
for our local developer meetup][1], and for that, I wanted .NET 8 Preview to run side by side with version 7 on my Mac. As
version 7 was initially installed with Homebrew, I also wanted to install version 8 Preview with Homebrew, but that
recipe was unavailable. Not perfectly happy with that, I fell back to the stand-alone installer, expecting
problems.

Installation went well, but then I turned to the command line only to find that `dotnet --list-sdks` was still and only
showing version 7. Yet, the 8 Preview was sitting there at its canonical location at `/usr/local/share/dotnet/sdk`,
where the v7 was also listed.

Puzzled, I tried a few things, but the quick fix was to simply `brew uninstall --ignore-dependencies dotnet` and, boom,
both versions 8 Preview and 7 became immediately available. I suspect that `brew uninstall` only removed the symlink
from .NET canonical location to the Homebrew cellar, which magically solved the SDK visibility problem. 

TL; DR. Homebrew recipes don't play nicely with .NET canonical installer. To make all my SDK versions visible to .NET,
I had to forego the Homebrew installation, which did not uninstall the SDK itself, but simply unlinked it.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or [follow me on Mastodon][m]*

 [1]: https://www.meetup.com/it-IT/devromagna/events/293340671/
 [rss]: https://nicolaiarocci.com/index.xml
 [m]: https://fosstodon.org/@nicola
 [nl]: https://buttondown.email/nicolaiarocci
