---
date: 2019-01-26T09:05:25+02:00
title: "NuGet Gems: DeepEqual"
share: false
---
This handy little package does one simple thing, and it does it well. According to its description, DeepEqual is:

> An extensible deep comparison library for .NET.

I am sure you too have come across this a few times. You have some code that shuffles around objects, and at some point, you'd like to make sure that two instances of the same class are, indeed, equal. And no, you don't mean "equal" as in [reference equality][re]. That's easy to achieve with .NET. Most of the time, what you want is to check for [value equality][ve].

Now, when it comes to value equality, there are a few things you can do in .NET: override `Object.Equals()` (which, by the way, if the type is a reference type, by default will check for reference equality), implement the `IEquatable` interface, override the `==` operator or, most commonly, a combination of these techniques.

The problem with this is, it can get messy real quick, especially if you are checking instances of non-sealed classes. Quoting the [documentation][note_for_callers]'s *Note for Callers*:

> When you call the Equals method to test for equality, you should know whether the current instance overrides Object. Equals and understand how a particular call to an Equals method is resolved. Otherwise, you may be performing a test for equality that is different from what you intended, and the method may return an unexpected value (source).

Sometimes you don't know the inner details about the classes you are playing with. Also, at least in my case, many times I am performing these checks in my tests, not in the application itself. Implementing all this comparison logic just for the sake of testing would be, in my opinion, overkill.

Sometimes (most of the times?), you only need to make sure two instances are equal by value, and very deeply at that. DeepEqual comes in handy:

    bool result = object1.IsDeepEqual(object2);

Simple as that. Again, I find this package invaluable especially when doing tests. Actually, I suspect I am *only* using it in my test. When used inside a test, you can call `ShouldDeepEqual`:

    object1.ShouldDeepEqual(object2);

This method throws an exception with a detailed description of the differences between the two objects. You can pass a custom comparison as the second argument to the `ShouldDeepEqual` method, to override the default behavior. You can also customize the behavior inline, using the `WithDeepEqual` extension method:

    object1.WithDeepEqual(object2)
       .SkipDefault<MyEntity>()
       .IgnoreSourceProperty(x => x.Id)
       .Assert()

I have been using this package for a long time. At some point, I even [submitted a pull request][pr] to port it to NetStandard. Despite a lot of people loving it, the pull request was left there unnoticed for quite some time. I was asked to release a fork, I declined (somebody else did). In the end, the package author came back from the void to release a new, NetStandard compatible, update, which is fantastic. Sometimes in open source, it takes a little patience.

Enjoy.

- [DeepEqual][de]

*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

 [tw]: http://twitter.com/nicolaiarocci
 [nl]: http://eepurl.com/b-_Pzz
 [de]: https://github.com/jamesfoster/DeepEqual
 [re]: https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/equality-comparisons#reference-equality
 [ve]: https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type
 [note_for_callers]: https://docs.microsoft.com/en-us/dotnet/api/system.object.equals?view=netframework-4.7.2
 [pr]: https://github.com/jamesfoster/DeepEqual/pull/27
