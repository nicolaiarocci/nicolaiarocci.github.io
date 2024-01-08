---
title: Introducing SimpleObjectCache a simple cross-platform object cache for .NET systems
author: Nicola Iarocci
date: 2016-07-20
url: /introducing-simpleobjectcache-a-simple-cross-platform-object-cache-for-net-systems/
categories:
  - Programming
tags:
  - .net
  - open source
---
[SimpleObjectCache][1] is a very simple permanent, cross-platform, asynchronous key-value object cache for .NET. It comes with built-in [SQLite 3][2] support. Alternative backends can be added by implementing the `IObjectCache` or `IBulkObjectCache` interfaces.

## How it works

First, you need to set the `ApplicatioName`. This is also going to be the folder where your cache will reside. Depending on the host OS the location of this folder might be different. On Windows it would be something like `C:\ProgramData\<ApplicationName>\SimpleObjectCache`.

Let&#8217;s instantiate SimpleObjectCache so we can use it:

{{< gist nicolaiarocci 8ad25dc8a892adb6a7428a3e5177edcd >}}

Now we create a `Person`, then store it into our cache.

{{< gist nicolaiarocci a45090fde90ce0fb210a1c000c9bd9ae >}}

As we insert an object into the cache we can also set its expiration date:

{{< gist nicolaiarocci 61e55e36e4e602a4ef025bf08df6617b >}}

Inserting an object with an already existing key, which we just did, will overwrite the previous object with the same key. Retrieving the object is a matter of providing its key:

{{< gist nicolaiarocci 30a890e120b10f0d4258d0e5f34e40f8 >}}

To remove the object from the cache we use the `Invalidate` method:

{{< gist nicolaiarocci 303a88046f0ad546f22eed84f45d6099 >}}

Bulk inserts are also possible:

{{< gist nicolaiarocci 2654b88bc3f7fe818dfa8ac862599728 >}}

Note that we just set the Tom and Mike expiration date to yesterday. Now let&#8217;s add John again. For him however, we set an expiration date which is bigger than Tom&#8217;s and Mike&#8217;s:

{{< gist nicolaiarocci abf9444dc7d87b175d6249506d5ef568 >}}

The `Vacuum` method removes expired objects from the cache. So Tom and Mike, whose dates are passed, are going to be purged by the following command:

{{< gist nicolaiarocci 729bf7604e06caacffbf761054829c74 >}}

Now let&#8217;s get all the available `Person` objects from the cache.

{{< gist nicolaiarocci a69e45d088d6d104ebe20a480405d6ba >}}

Since Tom and Mike are gone, we only got one object back, and that&#8217;s our very own little John.

## Installation

SimpleObjectCache is on [NuGet][3]. Run the following command on the Package Manager Console:

{{< gist nicolaiarocci 758165b8800d9dba483b8a50373d964c >}}

Or install via the NuGet Package Manager in Visual Studio.

## Wrapping it up

We needed a simple cache that we could use as a component of our cross-platform storage system (more on that in a future post). We wanted the cache to also run seamlessly on the old .NET 4.0 framework. Unfortunately [Akavache][4], to which this project is blatantly inspired, does not run on .NET4, so I decided to roll out my own simplified alternative. This project also offered a great occasion get my feet wet with bait-and-switch portable classes and a few other interesting challenges.

Currently supported platforms are iOS and Android (Xamarin) and .NET Framework versions 4.0 and .NET 4.5+.

If you want to get in touch, I am @[nicolaiarocci][5] on Twitter.

 [1]: https://github.com/nicolaiarocci/SimpleObjectCache
 [2]: https://www.sqlite.org
 [3]: https://www.nuget.org/packages/SimpleObjectCache/
 [4]: https://github.com/akavache/Akavache
 [5]: http://twitter.com/nicolaiarocci
