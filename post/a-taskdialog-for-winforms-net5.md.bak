---
date: 2020-04-19T09:05:25+02:00
title: "Rumors of Windows Forms death have been greatly exaggerated"
description: .NET 5 brings support for Windows Task Dialog to Windows Forms, and that is relevant for a number of reasons.
share: false
---

This morning on my twitter feed, this surprising tweet showed
up:

{{< tweet 1251480894436601857 >}}

Apparently, .NET 5 brings support for Windows TaskDialog to Windows Forms, and
that is relevant for several reasons. Before I dig in, let me start by
addressing your inevitable question right away. 

In essence, yes, Windows Forms is old technology. It has been around since like
20 years ago, and yes, newer Windows UI frameworks have (or try to have)
traction today, but no, that is not a good reason for Microsoft to let WinForms
rest in peace. See the thing is right now, as I am writing this piece, there
are *millions* of desktop applications running on Windows machines all around
the world and rest assured, an essential portion of them is running on, you
guessed it, your good old Windows Forms. 

I know first hand how essential is WinForms today. An application I wrote with
Forms many years ago, at the end of the 90s, still pays a good portion of my
income. Incidentally, that one application (along with its weight on my salary)
is why that single twitter stood out on my feed this morning.

Windows Forms is so relevant that it is now part of NETCore (soon to be
rebranded NET 5.) By the way, bringing Windows Forms into NETCore was
a monumental piece of work. At the time of this writing, the Designer (the main
reason, I think, behind Forms incredible success) is receiving its final touches
before the final release.

So with that out of the way, let me elaborate on why this tweet is important.
One thing is supporting an admittedly old technology for legacy reasons, and
a different one is to keep improving it. Yes, the NETCore port was great, but it was
just that, a port. We have not seen relevant new features such a long time that
everyone assumed nothing new was going to happen in this space. After all, it
makes sense with WPF, then UWP taking the stage in recent years. Then, out of
the blue comes this little precious new feature. 

It is not a coincidence that TaskDialog support comes as a community
contribution. The author is Konstantin Preißer
([@kpreisser](https://github.com/kpreisser)), and he improves on a little
fundamental pillar of Windows Forms, the MessageBox. Quoting from his [original
ticket](https://github.com/dotnet/winforms/issues/146):

> On Windows Vista and higher, the Task Dialog is available that provides many
> more features than a Message Box. While you can show a Message Box in
> WinForms and WPF, there is no "official" implementation of the Task Dialog
> yet in .NET WinForms/WPF (...) Do you think a Task Dialog could also be added
> directly to WinForms/WPF?


Now, this ticket dates December 4, 2018. That's almost one and a half years
ago. Since then, he's been hard at work. Then just yesterday, 169 commits, 59
files changed, [his pull request](https://github.com/dotnet/winforms/pull/1133)
was merged by Igor Velikorossov ([@RussKie](https://github.com/RussKie)) into
the official dotnet/winforms repository. Big props to Igor, by the way, who
spent all that time code-reviewing more than 10K lines of code.

So let's recap what we are dealing with here—one monster open-source,
community-driven contribution to an old, stagnant yet relevant Microsoft stack.
If, like me, you come from the "old Microsoft" era, you know how the previous
sentence would sound impossible only a handful years ago. To add to that, let's
ponder on Microsoft personnel taking the time to carefully peer-review, then
accept and merge the whole thing and, finally, celebrate the event on
social networks and whatnot:

> Thank you for your patience and commitment. We made the history my friend,
> the first major addition to Windows Forms in 15 years! Hope you have
> a champagne on ice, it is time to pop the cork. - [@RussKie on
GitHub](https://github.com/dotnet/winforms/pull/1133#issuecomment-615850774)

I think we can reasonably say that yes, the rumors of Windows Forms death have
been greatly exaggerated. That is primarily due to Microsoft going the full
monty on open-source and, secondarily, on the fantastic community that has been
growing around its core technology.

*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

 [tw]: http://twitter.com/nicolaiarocci
 [nl]: http://eepurl.com/b-_Pzz

