---
title: Introducing Eve.NET the HTTP/REST Client for Humans™
author: Nicola Iarocci
date: 2014-11-27
url: /introducing-eve-net-httprest-client-humans/
gr_overridden:
  - 1
gr_options:
  - 'a:3:{s:13:"enable-ribbon";s:4:"Show";s:10:"github-url";s:40:"https://github.com/nicolaiarocci/Eve.NET";s:11:"ribbon-type";i:5;}'
dsq_thread_id:
  - 3268007028
categories:
  - Programming
tags:
  - .net
  - c
  - eve
  - open source
  - python
  - rest
---
[Eve.NET][1] is a simple HTTP and REST client for Web Services powered by the [Eve Framework][2]. It leverages both `System.Net.HttpClient` and `Json.NET` to provide the best possible Eve experience on the .NET platform.

Written and maintained by the same author of the Eve Framework itself, Eve.NET is delivered as a portable library (PCL) and runs seamlessly on .NET4, Mono, Xamarin.iOS, Xamarin.Android, Windows Phone 8 and Windows 8. We use Eve.NET internally to power our iOS, Web and Windows applications. <!--more-->

_And now please forgive me while I take you on a quick motivational, strongly opinionated, probably boring and overzealous detour_

* * *

## Python and C# Motherfucker, Do You Speak It? *

If you don&#8217;t then well, you should consider doing just that. Especially so these days, with C# and the whole .NET platform going open source and cross platform. Actually, thanks to technologies like Mono and Xamarin (also based on Mono) we have been able to run C# code on all major platforms for a while: iOS, Android, OSX, Linux, Windows, Windows Phone, you-name-it. And what&#8217;s even better, on mobile platforms C# is compiled to native so performance is a non-issue.

What makes C# a perfect match for a REST API is precisely that: it&#8217;s ubiquity. You can have a portable client library like Eve.NET which runs seamlessly (and untouched) on all these mobile desktop and server platforms.

If you already have a Web Service running on Eve and are now looking at the client side of things then well, you should consider C# and Eve.NET because you know, you can&#8217;t have a native iOS app written in Python anyway. On the other hand if you are a C#/.NET shop consider this: you can have a powerful Web Service up and running in minutes (even if you don&#8217;t grok Python yet &#8211; trust me on that) _and_ a complete out-of-the-box, cross platform client library ready to go with it.

A few years ago I gave a talk about leaving my Comfort Zone (**) and getting out of my .NET nest. That opened the path to Python, MongoDB, Node and so many other technologies and best practices and, what&#8217;s even more relevant, most of what I learned down that path I ended up using in my .NET projects in the long run. But the point I&#8217;m trying to make is don&#8217;t be afraid of change, it can only improve your skills making you a better all-around professional programmer.

Never mind the naysayers. Polyglot is the way.

* * *

(*) I&#8217;m paraphrasing Zed A. Shaw&#8217;s [Programming, Motherfucker][3]. You should get a T-Shirt by the way. They are so cool.

(**) Since then there have been plenty of talks on the same subject. Mine was an 5 minutes ignite talk and was in Italian, so you probably don&#8217;t care (it&#8217;s on my [Talks][4] page anyway).

* * *

_Back to business now_.

## Usage

Initialization is as simple as instantiating a new client and providing it with the web service entry point.

    // Initialize and set API address.
    var client = new EveClient();
    client.BaseAddress = new Uri("http://api.com");
    
    // Set target resource for subsequent requests.
    client.ResourceName = "companies";
    

Getting a list of objects is pretty straightforward:

    // List<T>
    companies = await client.GetAsync<Company>();
    
    // Objects changed since DateTime.
    var ifModifiedSince = DateTime.Now.AddDays(-1);
    companies = await 
      client.GetAsync<Company>(ifModifiedSince);
    
    // Refresh an object
    company = await client.GetAsync<Company>(company);
    
    // Raw, conditional GET request
    var companyId = "507c7f79bcf86cd7994f6c0e";
    var eTag = "7776cdb01f44354af8bfa4db0c56eebcb1378975";
    
    company = await 
      client.GetAsync<Company>("companies", companyId, eTag);
    

Other CRUD operations are easy too:

    // Create (POST)
    company = await 
      client.PostAsync<Company>(
        new Company { Name = "MyCompany" }
      );
    
    // Update (PUT)
    company.Name = "YourCompany";
    var result = await client.PutAsync<Company>(company);
    
    // Delete (DELETE)
    var result = await client.DeleteAsync(company);
    

As you can see all methods are Async and return full object instances parsing JSON in and out on for you. If you need more control you can query the `HttpResponse` property to inspect the original JSON, response headers, status code, etc.

Behind the scenes [data integrity and concurrency control][5] are transparently handled so for example `PutAsync` performs a `If-Match` check and same happens with `DeleteAsync`. On `PostAsync` new objects are returned with fresh meta-fields such as `ETag`, `DateCreated`, `DateUpdated` and `UniqueId`. Mapping object properties to JSON fields and Eve metafields is just a matter of setting the `JSonPropertyAttribute` and `RemoteAttribute`:

    public abstract class BaseClass
    {
      [JsonProperty("_id")]
      [Remote(Meta.DocumentId)]
      public string UniqueId { get; set; }
    
      [JsonProperty("_etag")]
      [Remote(Meta.ETag)]
      public string ETag { get; set; }
    
      [JsonProperty("_updated")]
      [Remote(Meta.LastUpdated)]
      public DateTime Updated { get; set; }
    
      [JsonProperty("_created")]
      [Remote(Meta.DateCreated)]
      public DateTime Created { get; set; }   
    }
    
    public class Company : BaseClass
    {
      [JsonProperty("n")]
      public string Name { get; set; }
    
      [JsonProperty("p")]
      public string Password { get; set; }
    }
    

For a complete list of usage examples see the [README][6]

## Current Status and License

Eve.NET is a [Nicola Iarocci][7] and [Gestionali Amica][8] open source project distributed under the [BSD license][9]. It is a work in progress but it&#8217;s pretty stable already. It is [available on NuGet][10] as a pre-release package. The test suite can be run against a local Eve instance or, if you don&#8217;t grok Python yet, you can use a free test instance which is available online, see the [README][6] for details.

Did you read this far? Well thank you! And please, consider showing your appreciation by starring the project on [GitHub][1]. It feels so lonely out there.

If you want to get in touch, I’m [@nicolaiarocci][11] on Twitter.

 [1]: https://github.com/nicolaiarocci/Eve.NET
 [2]: http://python-eve.org
 [3]: http://programming-motherfucker.com/
 [4]: http//nicolaiarocci.com/talks
 [5]: http://python-eve.org/features#data-integrity-and-concurrency-control
 [6]: https://github.com/nicolaiarocci/Eve.NET/blob/master/README.md
 [7]: http://nicolaiarocci.com
 [8]: http://gestionaleamica.com
 [9]: https://github.com/nicolaiarocci/Eve.NET/blob/master/LICENSE.txt
 [10]: https://www.nuget.org/packages/Eve.NET/
 [11]: https://twitter.com/nicolaiarocci
