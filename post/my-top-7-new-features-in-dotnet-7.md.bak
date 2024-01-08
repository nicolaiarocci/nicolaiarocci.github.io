---
date: 2022-12-04T07:05:25+01:00
title: "My Top 7 New Features in .NET 7"
share: false
tags: ["dotnet", "csharp", "programming"]
---
The other day we did a [.NET 7 Spotlight][12] event at this month's
[DevRomagna][13] meetup. The speakers were [Ugo Lattanzi][14] and me. In my
session, I chose to talk about my top 7 new features in .NET 7 (pun intended.)
What follows is a mix of my preparation notes and what I ended up really
saying[^17].

## 1. Performance
Since the initial release of "new dotnet" (.NET Core), performance has always
been a critical goal for the .NET team. Starting with .NET 5, performance gains
have been skyrocketing. .NET 6 was *a lot* faster than 5, and now, well, I'm
surprised by the remarkable performance improvements in .NET 7. Stephen Toub
posted a remarkably long (255 printed pages!) [in-depth analysis of the
performance improvements in .NET 7][1]. one That was followed by articles
dedicated to [ASP.NET Core 7][2] and [MAUI 7][3] performance gains. At .NETConf
2022, a particular slide caught everyone's attention.

![](/images/dotnetconf22.png)

I recall seeing the same slide at the .NET 5 release, so this one is must be
updated version. I'm more impressed with the gRPC graph than the big "11x
faster than Node" one. Being faster than Node doesn't break the news these days,
but being quicker than Go, C++ and Rust? That's one bold statement you have
right there. 

An [exciting article][4] surfaced a while ago on this specific topic. In it,
Dustin Moris Gorski presents an in-depth analysis of the ASP.NET Core 7 code
used for the TechEmpower Framework Benchmark referenced in the above slide. The
results are... fascinating. That code is undoubtedly *not* what mere mortals
tend to run in their production systems. It is super-performance-optimized,
often ditching canonical, built-in, and wildly adopted features in favor of
low-level, high-performance and precisely hand-crafted alternatives. Dustin's
article is a masterpiece for several reasons; I suggest you invest your time
[reading it][4]. 

But yeah, despite this glitch, the takeaway is that .NET 7 is speedy, faster
than previous versions, and on par with, if not (far?) superior to, most stacks
and frameworks. The [Stephen Toub's article][1] is a testament to the massive
work done and the achievements obtained.

Most importantely, we get most of these speed benefits for free, just by
upgrading to .NET 7. And the good new is, the upgrade is as easy as changing
the framework moniker from, say, `net6.0` to `net7.0` and upgrading the
Microsoft dependencies to v7.0.0.

## 2. C# 11 `required` modifier
As a consequence of the C# release cycle alignment to that of.NET itself (which
is much faster), recent versions of C# see fewer features announcements than in
the past. A good thing in my opinion. Of the several appreciable new features
coming with C# 11, a remarkable one is the [`required` modifier][15]. 

When you enable nullable checks in a project, non-nullable string properties
are flagged with warning that they should be initialized with a non-null value
when exiting the constructor:

![](/images/required-keyword1.png)

A common workaround has been these properties them with a `null!` value. That
is like telling the compiler that we know they should be initialized with a
non-nullable, but well, let's initialize them with a null value first, just in
case. It'll all be sorted later in the code. Somewhat awkward and prone to
errors. Also, battling the compiler like that is a tedious task. 

Enter the `required` keyword. When you flag a property with `required,` the
IntelliSense engine will report an error if the property value is not set *at
initialization*, not at declaration. 

![](/images/required-keyword2.png)

When someone initializes our class instance, he/she's *required* to set an
explicit value for our property. Notice how we went from a warning (which
will compile) to an error (which won't compile). Once you start using this
feature, it feels so obvious and natural that you wonder why it wasn't there
right from start.

## 3. C# 11 raw string literals
In C# 11, wrapping a string with triple-double-quotes makes it a [raw
literal][5]. Its main benefits are that no escaping of double-quotes is
necessary, and newlines are allowed within the string. 

```
var xml = """
          <element attr="content">
            <body>
            </body>
          </element>
          """;
```

The code looks natural, and no runtime costs for specialized string
manipulation are required. One caveat is that string literals naturally remove
the indentation when producing the final literal value. The snippet above
prints as:

```
<element attr="content">
  <body>
  </body>
</element>
```

We can disable indentation removal like so:

```
var xml = """
          <element attr="content">
            <body>
            </body>
          </element>
""";
```

String interpolation is also supported:

```
var json = $$"""
             {
                "summary": "text",
                "length" : {{value.Length}},
             };
             """
```

In hindsight, like the `required` modifier, raw string literals appear as
obvious. 

## 4. Built-in container support
.NET 7 has [built-in container support][6], meaning that `dotnet publish` can
now output to a container image instead of a directory. We control image names,
tags, and other settings (like the base image) via dedicated `.csproj` tags. Two
requirements:

- Docker must be running when we issue the `publish` command;
- The `Microsoft.NET.Build.Containers` package must be added to the project as
  a package reference. 

In my demo, I had a small console application that I published to a docker
image by simply issuing the following command:

```
$ dotnet publish --os linux --arch x64 /t:PublishContainer -c Release
```

I did not mention a Dockerfile, and that's because it is not needed anymore.
All my projects deploy to docker containers and are already migrated to .NET 7.
I'm currently using Dockerfiles, but I'll be experimenting with this
alternative in the coming weeks, both with builds and remote CI builds.

## 5. Native AOT
[Native AOT][7] produces a standalone executable in the target platform's file
format, with no external dependencies. It's native, with no IL or JIT involved,
and provides fast startup time and a small, self-contained deployment. 

In my demo, I just needed to add a `<PublishAot>true</PublishAot>` tag to the
`.csproj`, and then the `dotnet publish -c Release` command produced a
single-file, macOS native executable. You can set the destination platform at
build-time like so: 

```
$ dotnet publish -r win-x64 -c Release
```

Native AOT will be determinant in a number of use cases, like
multi-cloud-deployments, lambda functions, and, in general, hyper-scale
services. ASP.NET Core is currently not supported, so we're limited to console
apps. 

## 6 and 7. Rate-limiting and output caching
Ok, these are two, not one. Luckily, my pal Ugo, who was demoing ASP.NET Core 7
parts after me, took charge of showing these. 

I briefly mentioned that rate-limiting and output caching are key features in
mature production systems. Until today, we had to bake them in-house or rely on
third-party packages. I've been using LazyCache and AspNetCoreRateLimit myself.
The latter [recently acknowledged][8] the arrival of rate-limiting in .NET 7 and
embraced it in a new package that offers Redis as a rate-limiting backend.
[Rate-limiting][9] and [output caching][10] are now part of the ASP.NET Core
framework, and that's where they belong. 

## 8. Minimal APIs group routes
I know I said 7. I don't use minimal APIs in production yet, but [group
routing][11] is beautiful and something I'll be employing on the first
occasion. During the meetup, an interesting (and much-expected) discussion
ensued on the usefulness of minimal APIs. Veterans of many battles don't deem
them necessary, especially in real-world use cases, which is actually accurate:
one can keep relying on the canonical MVC approach. The sentiment was that
Minimal APIs are mostly targeted to newcomers, which is probably true[^16]. As
someone coming from the Python REST ecosystem, I dig them a lot. They evolve
rapidly and I'm sure we'll soon see them in action in complex, real scenarios.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://devblogs.microsoft.com/dotnet/performance_improvements_in_net_7
 [2]: https://devblogs.microsoft.com/dotnet/performance-improvements-in-aspnet-core-7/
 [3]: https://devblogs.microsoft.com/dotnet/dotnet-7-performance-improvements-in-dotnet-maui/
 [4]: https://dusted.codes/how-fast-is-really-aspnet-core
 [5]: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-11.0/raw-string-literal
 [6]: https://devblogs.microsoft.com/dotnet/announcing-builtin-container-support-for-the-dotnet-sdk/
 [7]: https://learn.microsoft.com/en-us/dotnet/core/deploying/native-aot/
 [8]: https://github.com/stefanprodan/AspNetCoreRateLimit/issues/382
 [9]: https://devblogs.microsoft.com/dotnet/announcing-rate-limiting-for-dotnet/
 [10]: https://learn.microsoft.com/en-us/aspnet/core/performance/caching/output?view=aspnetcore-7.0
 [11]: https://learn.microsoft.com/en-us/aspnet/core/fundamentals/minimal-apis?view=aspnetcore-7.0#route-groups
 [12]: https://www.meetup.com/it-IT/devromagna/events/289709131/
 [13]: https://www.meetup.com/it-IT/devromagna/
 [14]: https://twitter.com/imperugo
 [15]: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/required
 [^16]: Back when Minimal APIs were about to debut, I wrote *[Will .NET 6 Minimal APIs turn heads?](https://nicolaiarocci.com/will-.net-6-minimal-apis-turn-heads?)*, with some musings on their effectiveness and target audience.
 [^17]: To Caesar what is Caesar's, short on time, I recycled both the idea and the materials from James Montemagno's [excellent video](https://www.youtube.com/watch?v=0BvCzZ9P7UY) on the same the topic.

 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
