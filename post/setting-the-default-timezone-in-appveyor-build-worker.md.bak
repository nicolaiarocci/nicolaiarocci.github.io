+++
date = "2017-02-25T16:48:09+01:00"
title = "Setting the default timezone in AppVeyor build worker (and C# 7.0 support)"
slug = "setting-the-default-timezone-in-appveyor-and-c-sharp-7-support"
tags = [".net", "appveyor"]
+++
So yesterday I pushed some code over to GitHub, then went off to work on
a different project. A few seconds later I got an email from [AppVeyor][2]
telling me that my CI build worker was reporting a failure. I was surprised as
just ahead of the push I had tests all green in local.

Turned out failure was on an equality assertion between two date values:

![](/images/appveyor-failure-on-date-fields.png)

As you can see the mismatch was *precisely* two hours. That always rings a Time
Zone alarm bell in my head. I was under the assumption that since my time zone
was correctly set in my account settings, the workers would pick it up. Well as
it turns out, that is not the case as that setting is only used for
notifications and NuGet feeds. The AppVeyor app worker runs on UTC by default. 

Solution was straightforward. I edited the `appveyor.yml` file and instructed
the worker to launch `tzutil` and set the desired time zone immediately, before
anything else is executed:

{{< gist nicolaiarocci afbce25a393067e3e22e2f3f706f548a >}}

And that was it. Remember, you can use `tzutil /l` on your local box to get
a list of the available timezones. 

Another minor (and temporary) issue I have with AppVeyor is that they do not
officially support C# 7.0 yet. Try using an inline temporary variable in your
code. Tests will be green in local and happily fail on AppVeyor, as the VM runs
MSBuild 14. The Visual Studio 2017 RC image is in beta and not available in the
Environment settings unless you explictly ask for it [here][1]. They are quick
to reply though and then, not without some more fiddling (see the post at the
top of the thread), you can get C# 7.0 features to run seamlessly in the VM.


*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

 [1]: https://github.com/appveyor/ci/issues/1179
 [2]: https://www.appveyor.com
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: http://eepurl.com/b-_Pzz
