+++
date = "2017-02-18T10:48:29+01:00"
title = "Python Workload pulled off Visual Studio 2017 RC3"
tags = ["visual studio", "python"]
+++

So how do you install the awesome [Python Development Tools][1] on the latest
Visual Studio 2017 RC? That might seem a stupid question considering that the
Data Science and Python Development workload has been available with every
Release Candidate so far. You simply select the workload during the
installation and you're done, right? Not quite. 

I found out the hard way this morning as I wanted to install VS 2017 RC3 on my
development machine and, to my surprise, I could not find Python Development
anywhere on the workloads window (which itself is a huge improvement over the
VS 2015 install experience, by the way). Easy, I thought, they moved it to some
secondary "optional workloads" tab, but a quick scan did not reveal any of
that.

Concerned now, I turned to the [Oracle of All Things][2] only to find that the
Python Workload has been pulled off the Visual Studio 2017 RC3 (January 2017).
It was actually reported in the [release notes][3]:

> Removed the Data Science and Python Development workloads as some of the
> components weren’t meeting the release requirements, such as translation to
> non-English languages. They will be available soon as separate downloads. 

When I glanced over them I (and probably you too) did not notice this little
paragraph. But wait, it's even worse than you would expect:

> Upgrading to current version will remove any previously installed Python and
> Data Science workloads/components.

That's right. If you upgrade to RC3 you win a wipe out of your Python
environment. Further research revelead an open [ticket][4] on GitHub.
Apparently they are working on a way to install the Python and Data Science
workloads on top of an existing VS 2017 install, but I would not hold my breath
on it:

> Thanks everyone for the support and understanding. It's still not clear to us
> how we're going to be releasing Python support, but the plan is definitely to
> have something when VS 2017 releases next month. 

Since the official VS 2017 release is planned early next month it is very
likely that we will just have to wait until then. In the meantime, you better
have a VS 2015 sitting side by side with your brand new, mutilated, Visual
Studio 2017. Or you switch to Visual Studio Code, which offers fantastic
support for Python. 

Or you fallback to good ole trusted Vim, like I did.

UPDATE (Feb 22, 2017). There's now an [official post][5] up at the Microsoft
Python Engineering blog, by Steve Dower. Looks like using Python with Visual
Studio 2017 will initially require a separate "preview" build of VS itself.
Only months later Python support will be merged to the official bundle. 

UPDATE (Mar 8, 2017). I posted a [follow-up article][6], as VS2017 has finally
been released.

*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

[1]: https://www.visualstudio.com/vs/python/
[2]: https://www.google.com/?gfe_rd=cr&ei=Lh2oWNCJENCv8wfrtaqYDA&gws_rd=cr#q=python+tools+visual+studio+2017+rc3
[3]: https://www.visualstudio.com/en-us/news/releasenotes/vs2017-relnotes
[4]: https://github.com/Microsoft/PTVS/issues/2099
[5]: https://blogs.msdn.microsoft.com/pythonengineering/2017/02/22/python-in-vs2017/
[6]: https://nicolaiarocci.com/python-support-in-visual-studio-2017-or-the-lack-thereof/


[tw]: http://twitter.com/nicolaiarocci
[nl]: http://eepurl.com/b-_Pzz

