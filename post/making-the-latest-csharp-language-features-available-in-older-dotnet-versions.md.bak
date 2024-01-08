---
date: 2023-02-04T07:05:25+01:00
title: "Making the latest C# language features available in older .NET versions"
slug: making-the-latest-csharp-language-features-available-in-older-dotnet-versions
share: false
tags: ["til", "dotnet", "programming", "polysharp"]
---
In a C# library I've been working on, I wanted to use C# 9.0's `init` keyword.
Quoting the [documentation][3]:

> The init keyword defines an accessor method in a property or indexer. An
> init-only setter assigns a value to the property or the indexer element
> **only** during object construction. This enforces immutability so that once
> the object is initialized, it can't be changed again.

Consider the following class:

```
    public class Person
    {
        public string FirstName { get; init; }
    }
```

You can initialize it like this:

```
    var person = new Person { FirstName = "John" };
```

But this will fail:

```
    var person = new Person();
    person.FirstName = "John";  //Not allowed
```

For my project, which is a .NET Standard 2.0 library, I thought this approach
might be preferable to a parameter-enforced class constructor alternative.

To my surprise, however, when I tried the above, I got the following error:

```
The predefined type 'System.Runtime.CompilerServices.IsExternalInit' must be
defined or imported in order to declare init-only setter
```

As it [turns out][1], The `IsExternalInit` type is only included in the net5.0
(and subsequent) target frameworks, so one cannot use it right away in a
NetStandard 2.0 (or 2.1, for that matter) library. 

In the dotnet world, when I encounter *"type is not defined in version X"*
scenario, I know I can get around the issue by making up the type on my own. A
quick lookup confirmed that this was the case, and the workaround is to add
the following somewhere in my source code:

```
    namespace System.Runtime.CompilerServices
    {
        internal static class IsExternalInit {}
    }
```

And presto, the `init` keyword is now fully available to my library.

While researching this matter, I stumbled into [PolySharp][2],  a lovely
package that takes this workaround approach to new heights. What is it?

> PolySharp provides generated, source-only polyfills for C# language features,
> to easily use all runtime-agnostic features downlevel. The package is
> distributed as a source generator, so that it will automatically detect which
> polyfills are needed depending on the target framework and project in use:
> just add a reference to PolySharp, set your C# language version to latest,
> and have fun!

And it works! Just add a PolySharp reference, and almost all modern C# language
features become automagically available to your project, with no tricks around
polluting your code. What's also nice about PolySharp, is that it isn't a
dependency for your library; it only needs to be there at compile time.

Do you know what's funny? After all, I took a different route; no `init`
keyword is used anymore in my library, but that's for another story.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or [follow me on Mastodon][m]*

 [1]: https://developercommunity.visualstudio.com/t/error-cs0518-predefined-type-systemruntimecompiler/1244809#TPIN-N1249582
 [2]: https://github.com/Sergio0694/PolySharp
 [3]: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/init
 [rss]: https://nicolaiarocci.com/index.xml
 [m]: https://fosstodon.org/@nicola
 [nl]: https://buttondown.email/nicolaiarocci
