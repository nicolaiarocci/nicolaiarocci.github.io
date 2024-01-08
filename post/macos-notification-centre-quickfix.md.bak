+++
date = "2018-04-12T10:06:35+02:00"
share = false
title = "Mac Notification Center does not work: the Quick Fix"
+++
I had this happen to me a few times already. Notification Center on the Mac
goes completely numb: no more notifications and the list is empty. I'm writing
down the fix, so I do not have to google the forums once again the next time.

Open the Terminal, then:

    # this usually fails, as the notification server is already running
    launchctl load -w /System/Library/LaunchAgents/com.apple.notificationcenterui.plist

    # kills and restarts the notification center - fixed!.
    killall NotificationCenter


*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

 [tw]: http://twitter.com/nicolaiarocci
 [nl]: http://eepurl.com/b-_Pzz

