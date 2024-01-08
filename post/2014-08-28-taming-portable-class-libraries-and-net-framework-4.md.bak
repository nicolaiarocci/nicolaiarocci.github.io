---
title: Taming Portable Class Libraries and .NET Framework 4
author: Nicola Iarocci
date: 2014-08-28
url: /taming-portable-class-libraries-and-net-framework-4/
dsq_thread_id:
  - 2998160399
categories:
  - Programming
tags:
  - .net
  - installshield
  - kb2468871
  - pcl
---
If your project is a Portable Class Library and you want it to run with the .NET Framework 4 well, you are in for a few surprises. Especially so if you are using InstallShield for building your deployment package. We&#8217;ve been going through this a few days ago and it&#8217;s been kind of a wild ride. I thought I could pin the whole thing down so that others might enjoy a painless journey through all this mess.

## Portable Class Libraries and .NET Framework 4

The first thing you should know is that while the .NET Framework 4 does support PCLs, in fact it won&#8217;t run them without a patch. For whatever reason, Microsoft decided that PCL compatibility wasn&#8217;t a worth a 4.0.4 update. That leaves us with the need to not only make sure that target machines are running the up-to-date .NET4 release (v4.0.3) but also that they&#8217;ve been updated with <a href="https://support.microsoft.com/kb/2468871" target="_blank">KB2468871</a>.

You might be wondering why this is an issue in the first place. We could simply install the .NET Framework 4.5 which is backward compatible with the .NET4 and includes the afore mentioned KB2468871. Even better, we could just target the .NET 4.5 on our PCL. Problem is that besides iOS, Android, WinPhone and Silverlight we also want our libraries to run seamlessly on as many Windows editions as possible, Windows XP included. Here is the catch: <a href="https://connect.microsoft.com/VisualStudio/feedback/details/730732/net-framework-4-5-should-support-windows-xp-sp3," target="_blank">.NET4 is the last framework version to run on Windows XP</a>. And yes, we got the memo, Microsoft officially abandoned Windows XP a while ago so why bother? Well it turns out that millions of users are still running XP, especially so in the enterprise and SMB. These PCL are targeting exactly that, precisely the accounting software segment, and believe me there&#8217;s a huge number of users happily invoicing and accounting on their _old-fart-but-still-splendidly-doing-its-job-for-cheap_ boxes. Oh and the .NET Framework 3.5 is not an option as it doesn&#8217;t support Portable Classes at all. <!--more-->

All things considered, it&#8217;s still good news. We can build PCL which run everywhere, Windows XP included. We only need to make sure that both the .NET Framework 4 and the KB2468871 are installed on target machines. Easy enough, right?

## The strange story about KB2468871 InstallShield Prerequisite

We rely on InstallShield for building our distributions, so I was delighted to find that it comes with a KB2468871 Setup Prerequisite out of the box. All we had to do was add the prerequisite to our setup and we would be done. In fact, our first test was encouraging. We ran the setup on a pristine Windows XP. It installed the .NET Framework 4, then the KB patch and then, finally, our own application which included the PCL libraries. Everything was running smoothly. We then moved on to test the same identical build on a fresh Windows 7 machine. Again, it installed the .NET4 just fine&#8230; and then it crashed. Actually, the setup itself did not crash. It was the KB2468871 which was crashing while the main setup itself was left idle, waiting for the KB install to complete. So, what was going on there?

### CPU Architecture Does Matter

To make a long story short, after a lot of investigation and an embarrassingly high number of tests we found that our setup was only crashing on 64bit editions of Windows. It turned out that the issue was with the InstallShield Prerequisite itself. It was broken. In a bad way.

The KB2468871 comes in three flavors:

  * NDP40-KB2468871-v2-x86.exe
  * NDP40-KB2468871-v2-IA64.exe
  * NDP40-KB2468871-v2-x64.exe

Three executables, each one targeting a different architecture. Upon inspection of the stock prerequisite however, we discovered that it was launching the x86 executable no matter what the target edition of Windows was. That explained the crashes on x64 systems.

The solution was to create a new custom prerequisite which would download and launch the x64 KB edition on 64bit systems. We then had to update the stock prerequisite too, so that it would only run on x86 systems. So we now had two specialized KB2468871 prerequisites. One for 32 and another for 64 bit systems. They would be launched alternatively depending on the target system. We proceeded to add them both to our InstallShield project and rebuild it. Then we went and tested it against freshly installed Windows. It installed the .NET Framework 4, then totally skipped the KB (like the prerequisite didn&#8217;t even exist) and finally proceeded to install both PCL and main application &#8211; which of course would crash on execution as there was no KB on the system.

Beaten, but not ready to admit defeat yet, we went back to the drawing board.

### Execution Order Does Matter. Or Not.

Our custom launch conditions for both our KB prerequisites were there, and they looked good. Then there was this other conditional triplet. It was validating two registry keys and then making sure that mscorlib.dll existed in .NET4 folder. So, the idea was that the KB installation should only be executed if the .NET4 was on the target system. That sounded perfectly reasonable. As we could configure the order in which prerequisites were executed, we just had to make sure that the .NET4 prerequisite was assigned a higher priority, so it would run before the KB prerequisites themselves. The prerequisites order was fixed, a new setup was built and&#8230; nothing changed. KB were still not being installed.

Prerequistes order did not seem to matter. In fact, if we removed that check-if-net4-is-there conditional triplet the KB would install. However that was not an acceptable solution because then the KB would _always_ be installed, causing a reinstall (and a waste of time and resources) on most systems.

Then I had my epiphany. Maybe launch conditions were being evaluated all together at boot time, for all prerequisites, before they were installed and regardless of their execution order? Non-sense you might think (I did). Why allow me to set an execution order in the first place, if launch conditions for each item are not going to be evaluated in _that_ order? Luckily, validating this theory was going to be quick and easy. We just had to reboot the system after the faulty installation was completed, then run the setup again. And guess what? On second run, after the reboot, the KB installation would be executed without a glitch. Bingo. Since the .NET4 had been installed on the previous run, now registry keys were there and the mscorlib.dll was in the right place, so the KB launch conditions were finally met.

We ended up replacing that bogus conditional triplet completely and changing the validation logic. Instead of checking if the .NET4 was installed (on pristine XP and Windows 7 systems, which don&#8217;t have the .NET Framework 4 preinstalled, _it just could not be there_ _yet_), we were now simply checking if KB itself was installed. After all it just needs to be there, no matter the Windows or framework version (on .NET 4.5+ the KB will be installed by default).

So now, armed with our brand new custom KB2468871-x64 prerequisite and a totally re-imaginated set of launch conditions we were finally able to build a setup that would deliver a fully functional Portable Class Library which would run on all possible Windows: XP, Windows 7, Windows 8&#8230; independently of the CPU architecture. Victory!

If you read this far you probably noticed that I didn&#8217;t include instructions on how to apply these changes to the stock prerequisite, let alone create a new one. You can find those instructions on the InstallShield website, or you can simply use [our modified prerequisites][1]. Of course we are providing them without any guarantee that they will work for you. They did for us, and that&#8217;s it.

## Too long; didn&#8217;t read

  1. Portable Class Libraries won&#8217;t run on plain vanilla .NET Framework 4.0 unless KB2468871 is installed;
  2. If using InstallShield KB2468871 Setup Prerequiste you&#8217;re in for a wild ride;
  3. However, and until an official fix is released, you can opt to use our modified prerequisites instead.
  4. Get the [custom KB2468871 (64x) InstallShield prerequisite][2].
  5. Get the [custom KB2468871 (x86) prerequisite][3].

## Conclusion

The stock KB2468871 InstallShield prerequiste has been out for a good while so I&#8217;m baffled that to this day I still cannot find any reference about these issues on the internet. Portable Class Libraries are probably still a niche and the fact that most of Macrovision KB resources are hidden behind a wall does not help. Soon or later an official prerequisite update will be released. Until then, feel free to use our mods.

I&#8217;ll just add that if we were dealing with an Open Source project, we&#8217;d just open a pull request and be done with it.

If you want to get in touch, I&#8217;m [@nicolaiarocci][4] on Twitter.

 [1]: https://gist.github.com/nicolaiarocci/34f9c167a4ec1adf591a
 [2]: https://gist.github.com/nicolaiarocci/34f9c167a4ec1adf591a#file-microsoft-net-framework-4-0-kb2468871-x64-prq
 [3]: https://gist.github.com/nicolaiarocci/34f9c167a4ec1adf591a#file-microsoft-net-framework-4-0-kb2468871-prq
 [4]: https://twitter.com/nicolaiarocci
