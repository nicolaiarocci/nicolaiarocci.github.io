---
date: 2023-10-25T07:05:25+01:00
title: "LINQ DistinctBy on a property for .NET Standard and older .NET versions"
slug: linq-distinctby-on-a-property-for-dotnet-standard-and-old-dotnet-versions
share: false
tags: ["til", "dotnet", "csharp", "programming"]
---
Today I learned how to implement a custom `Enumerable.DistinctBy` extension method that returns distinct elements from a
sequence according to a specified key selector function.

.NET 6 and its successors have the method [built in][1] within LINQ, but I needed it in a .NET Standard 2.0 class
library, so I was out of luck. My implementation is simple, not different from [others][2] I found online, and should
also work fine with old .NET releases. Here it is:

```
    public static IEnumerable<TSource> DistinctBy<TSource, TKey>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector)
    {
        var keys = new HashSet<TKey>();
        foreach (var element in source)
        {
            if (keys.Contains(keySelector(element))) continue;
            keys.Add(keySelector(element));
            yield return element;
        }
    }
```

In the following usage example, I will get back all unique objects from the original sequence, distinct by their Name
property:

```
    var uniques = mySequenceOfObjects.DistinctBy(x => x.Name);
```

I later went to check the [official .NET 6+ implementation][3]. They support an optional equality comparer , which I
don't need, but their base implementation is similar to mine (they use deferred execution as well). 

By the way, years after its open-sourcing, I still get thrills when I realize I can always look at, let alone contribute
to, the .NET source code.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or [follow me on Mastodon][m]*

[1]: https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.distinctby?view=net-6.0
[2]: https://stackoverflow.com/a/489421/323269
[3]: https://github.com/dotnet/runtime/blob/e0409d44bd8d1fd0be1d66fbb52bd609be18f388/src/libraries/System.Linq/src/System/Linq/Distinct.cs#L62
 [rss]: https://nicolaiarocci.com/index.xml
 [m]: https://fosstodon.org/@nicola
 [nl]: https://buttondown.email/nicolaiarocci
