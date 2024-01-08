+++
date = "2017-05-10T09:47:05+02:00"
share = false
title = "How to convert a PCL (Portable) project to NetStandard"
tags = [".net", "netstandard", "visual studio"]
+++
I have been upgrading a few projects from their original PCL profiles (now
deemed obsolete) to the [Net Standard][1] platform specification. It turned out
to be a relatively straightforward process, but it does have its small hurdles,
especially so if in the meantime you also want to transition to the new,
streamlined, `.csproj` format as the migration will leave you with a now
obsolete `project.json` project. In this article, I will cover upgrading
a project from Portable Class Library to NetStandard. In a follow-up post,
I plan to write about the switch from `project.json` to the new `.csproj`
format.

So let us take the [Eve.NET][2] project as an example. It makes a good
candidate because it is an open source project, so you can go and have a look
at the source code [before][4] and [after][3] the switch from PCL to
NetStandard. 

The first step was, of course, opening the project in Visual Studio 2017. If
you are on an older VS version, you should upgrade. For many valid reasons
indeed, among them the fact that Visual Studio 2017 comes with a built-in
option to switch a project to NetStandard. 

![](/images/netstandard1.png)

As you can see, before the upgrade Eve.NET was a Profile259 PCL project. As
metioned, Visual Studio offers the option to switch to the .NET Platform
Standard. By clicking the link, you get a fair warning that *you might not be
able to use the same APIs when targeting NetStandard*. That makes sense
because, as you probably know already, NetStandard is an API specification
while a PCL essentially is the intersection (or lowest common denominator) of
the APIs available on target platforms. PCL compatibility has never been the
design goal of NetStandard. 

Generally speaking, NetStandard offers a wider range of APIs compared to most
PCL profiles and, most importantly, is planned to go through a cycle of
incremental upgrades of the API specification, each one denoted by a version
number. We already went from 1.0 to 1.6, with 2.0 currently being developed.
[NetStandard 2][5] will be a significant milestone, just give a look at the
[impressive diff][6] between 1.6 and 2.0. A *lot* of open source projects are
eagerly waiting on NetStandard 2 release (Q3 2017).

Upon confirming the switch, you might get the following show-stopper (I did):

![](/images/netstandard2.png)

This dialog will pop up if your project never has opted-in for NuGet 3.0. If
this is the case, you have to go back, uninstall all NuGet packages, then
attempt the switch again. When the migration is complete, you will have to
re-install the packages, provided that they are compatible with NetStandard. In
Eve.NET case the only dependency is Json.NET, which supports NetStandard 1.3,
which also means that Eve cannot support previous NetStandard versions.

Now, if you give a look at the installed packages, you will find that you have
a couple of new entries: `NETStandard.Library`, which is pretty
self-explanatory, and `Microsoft.NETCore.Portable.Compatibility`. This one will
only appear when you convert from a PCL: a brand new NetStandard project will
not take a dependency on it. If you are not using any legacy code, like NET
4.0-only, or Silverlight, you should be able to drop this dependency safely (I
did with no consequences).

The project is now NetStandard and ready to be used on all the platforms
supporting your chosen version: NETCore, Windows, Xamarin, UWP, you name it.

However, you will soon notice that the project has gained a `project.json`
file. It is ok, it works just fine, but it is obsolete: with Visual Studio 2017
project.json was abandoned for a new, streamlined and pretty darn powerful,
`.csproj` project file. In the next article, I will show you how to move your
project forward by dropping `project.json` and embracing the new project type
(and other niceties, like dropping the `.nuspec` file in the process).

*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

[tw]: http://twitter.com/nicolaiarocci
[nl]: http://eepurl.com/b-_Pzz
[1]: https://docs.microsoft.com/it-it/dotnet/articles/standard/library
[2]: https://github.com/pyeve/Eve.NET/
[3]: https://github.com/pyeve/Eve.NET/tree/netstandard
[4]: https://github.com/pyeve/Eve.NET/tree/v0.2
[5]: https://github.com/dotnet/standard/blob/master/docs/netstandard-20/README.md
[6]: https://raw.githubusercontent.com/dotnet/standard/master/docs/versions/netstandard2.0_diff.md
