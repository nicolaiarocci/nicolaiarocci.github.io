---
date: 2021-12-11T07:05:25+01:00
title: "Migrating a Windows 10 VM to Windows 11 in Parallels Desktop: a story of TPM chips and BIOS upgrades"
share: false
tags: ["til", "windows11", "parallels"]
---
This weekend assignment was to upgrade a couple of old Windows 10 VMs to
Windows 11 in Parallels Desktop 17. I couldn't do that right away because
Windows Update was complaining about the lack of the TPM chip. A little
research revealed that TPM chips only work on UEFI BIOS.  To check which BIOS
version was being used in my VMs, I used the msinfo32 (System Information)
application. It showed the BIOS to be of "Legacy" type. So my task was now to
switch it to UEFI.

![Windows 10 BIOS in Legacy  mode](/images/windows10-bios-legacy-mode.png)

I looked high and low with little luck. Parallels the product is incredible.
Not so much its documentation and online support.  At some point, I landed in
the Parallels forums, a vast ocean of scarcely useful threads from which
I usually try to stay the hell away. The Parallels personnel there has
a long-standing tendency to copy & paste ready-made and irrelevant solutions.
Users are left to their own, and, luckily, one of them posted the [perfect
solution][1] to my Legacy-to-UEFI BIOS migration problem. I am reposting it
here, with minor edits, for future reference (my future self [will be
grateful][2]):

1. Back up your VM
2. Boot into your Windows 10 VM as usual
3. While holding down Shift key: Start -> Power -> Restart
4. Select Troubleshoot, then Advanced options
5. Select Command Prompt
6. Log in with your account and Microsoft password (not your pin)
7. Type: `mbr2gpt /validate` and hit return; this will check your hard disk
8. If there's a problem, type: `mbr2gpt /validate /allowFullOS` and hit return
9. Type `mbr2gpt /convert` and hit return. It will convert the MBR disk partition scheme to GUID. It might complain about WinRE or something, but generally, if it says "conversion was a success," you can type `exit` and hit return to kill the command prompt and return to the advanced menu
10. Choose "Turn off PC." You don't want to restart Windows yet
11. Find your VM file in the Finder, right-click on it, and choose: "Show Package Contents."
12. Find the config.pvs file and open it with a text editor
13. Search for the section `<Bios dyn_lists="">`
14. Change `<EfiEnabled>` from 0 to 1
15. Change `<EfiSecureBoot>` from 0 to 1
16. Save the file
17. Open the VM Configuration, go to the Hardware tab, click the "+", and add the TPM Chip

At this point you can run Windows 10 as you usually would. At fist launch,
right after the login, I got a critical error and a hard restart (the original
poster reported the same experience.) After that, the VM is stable. A quick
msinfo32 check confirms that the VM is now on UEFI BIOS. 

![Windows 10 BIOS in UEFI mode](/images/windows10-bios-uefi-mode.png)

Should Windows Update still complain, that's probably because of the CPU
limitation check. You can disable it:

1. Open the Registry Editor 
2. Navigate to `HKEY_LOCAL_MACHINE\SYSTEM\Setup\MoSetup`
3. Search for `AllowUpgradesWithUnsupportedTPMOrCPU`
4. Change its value to 1
5. Restart the VM

Personally, I did not need to alter the registry, and I got *very* old VMs to
upgrade. At the time of this writing, Windows 11 installation is at 94% and
I am confident it will be successful.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://forum.parallels.com/threads/process-for-converting-from-legacy-to-uefi-in-prep-for-win-11.354888/
 [2]: https://nicolaiarocci.com/learn-in-public/
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
