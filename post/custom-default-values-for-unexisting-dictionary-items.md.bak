---
date: 2021-06-11T07:05:25+01:00
title: "Custom default values for not existing dictionary items (and a lesson learned)"
share: false
tags: ["til", "dotnet", "programming"]
---
When dealing with dictionaries, a typical problem is when an operation attempts
to retrieve an element using a key that does not exist in the dictionary. In
.NET, a `KeyNotFoundException` is raised, and that's the desired behaviour in
most circumstances. Sometimes, however, you know that your program will
frequently try to retrieve keys that do not exist. In such cases, it is more
efficient to use the `TryGetValue` method:

> This method returns the value associated with the specified key, if the key
> is found; otherwise, the default value for the type of the value parameter is
> returned ([source][1])

The devil hides in details. `TryGetValue` returns the default value for the
type of the `value` parameter. So, if you use `TryGetValue` to look into
a dictionary of strings, `null` is returned on a missing key. That is probably
ok in most cases. Howewer, if your logic requires a custom default value
instead, then you are out of luck. You have to set it yourself on `TryGetValue`
failure. A typical implementation would be:

```
    var result = MyDictionary.TryGetValue("key", var out value) 
        ? value
        : "not found";
```

It is a minor annoyance but still a hassle. Our solution has always been
a homemade `GetValueOrDefault` extension method, something like this: 


```
    public static TValue GetValueOrDefault<TKey, TValue> 
        (this IDictionary<TKey, TValue> dictionary, TKey key, TValue defaultValue)
    {
        return dictionary.TryGetValue(key, var out value) 
            ? value
            : defaultValue;
    }
```

Usage:


```
    var result = MyDictionary.GetValueOrDefault("key", "not found");
```

We've been using it since forever, and we are still using it even in recent
projects.

Today, as I was looking at something only tangentially related, I learned that
our extension method is obsolete, and it's been for a while. NetStandard
2.1 and NetCore 2 added a new extension method to the official API. It's
called, you guessed it, [`GetValueOrDefault`][2]. It extends
`ÌReadOnlyDictionary<TKey, TValue>`, so it applies to all generic dictionaries,
which is cool.

We could continue with our extension method. It has the advantage of working
across all .NET platforms, not just recent ones. Implementations are likely
similar, and there’s probably little (if any) performance difference (I am too
lazy to compare). With NETCore (now NET5), APIs have not only acquired
cross-platform compatibility and improved performance but they have also been
expanded and amended, something often not very apparent. Not to me, at least.

The point I want to make here, I think, is that nothing is set in stone. Today's
little event shows how my knowledge becomes stagnant over time. Setting apart
the time to learn new things is good, but acquired ones need sharping too.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2.trygetvalue?view=net-5.0
 [2]: https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.collectionextensions.getvalueordefault?view=net-5.0

 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
