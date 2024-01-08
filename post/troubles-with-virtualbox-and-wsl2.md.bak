---
date: 2021-02-14T07:05:25+01:00
title: "Troubles with VirtualBox and the Windows Subsystem for Linux"
share: false
tags: ["linux", "windows10", "virtualbox"]
---
Today I learned the hard way: don't you dare running a vanilla install of
VirtualBox together with Windows Subsystem for Linux v2 (WSL2). It won't work.
That's because WSL2 uses Hyper-V under the hood, which is incompatible with
VirtualBox. 

According to the [official documentation][1] for VirtualBox v6.0:

> Oracle VM VirtualBox can be used on a Windows host where Hyper-V is running.
> **This is an experimental feature**. No configuration is required. Oracle VM
> VirtualBox detects Hyper-V automatically and uses Hyper-V as the
> virtualization engine for the host system. 

Well, that did not prove to be true in my case. Hence the experimental clause,
I guess. A little googling revealed that, indeed, it did work for a while, then
a new Windows 10 release broke it again:

> The Hyper-V API became a viable reality with 1803, practically with 1809. And
> it went fine with 1903. And it broke with 1909. Please use your favorite
> search engine for "Immature API"... ([source](https://forums.virtualbox.org/viewtopic.php?f=6&t=90853&start=195#p465333))

Even if it did work, however, you'd run into some (possibly) severe
performance degradation. Quoting from the same official documentation page:

> When using this feature, some host systems might experience significant
> Oracle VM VirtualBox performance degradation.

If you don't need to run WSL2 and your VMs simultaneously, one workaround is to
disable WSL2 in the Windows Features.  There, you have to disable Hyper-V,
Virtual Machine Platform, and Windows Subsystem for Windows. Yes, I had to
explicitly disable all three of them. When you eventually reactivate them, WSL2
will start working again, configurations included.

Another option is to fallback to WSL1. That will work. Unlike WSL2, WSL1 does
not run in a VM. Also, converting back and forth between WSL1 and WLS2 is dead
simple. I did not go this route because, well, I like the performance that
comes with WSL2. I also plan to use VirtualBox only rarely, when I need to test
new versions of our desktop application's installation procedure.

This is all not ideal, of course. The situation is evolving. [This ticket][2]
on the WSL documentation repository is probably the place to watch for updates.

Hopefully, soon, once the currently "immature API" stabilizes, I will be able
to come back to this article, edit it, and note that now everything works as
expected.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [2]: https://github.com/MicrosoftDocs/WSL/issues/536
 [1]: https://docs.oracle.com/en/virtualization/virtualbox/6.0/admin/hyperv-support.html
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
