---
title: 'Feature Overview: The Eve OpLog'
author: Nicola Iarocci
date: 2014-10-06
url: /feature-overview-the-eve-oplog/
dsq_thread_id:
  - 3087578057
categories:
  - Programming
tags:
  - eve
  - python
---
The operations log or OpLog is a new [Eve][1] feature that I&#8217;m currently developing on the [`oplog`][2] experimental branch. It&#8217;s supposed to help in addressing a subtle issue that we&#8217;ve been dealing with, but I believe it can also emerge as a very useful all-around tool. I am posting about it in the hope of gathering some feedback from Eve contributors and users, so that I can better pinpoint design and implementation before I merge it to the main development branch.

## What is the OpLog?

The OpLog is a special resource that keeps a record of operations that modify the data stored by the API. Every `POST`, `PATCH`, `PUT` and `DELETE` operation can eventually be recorded by the oplog.

At its core the oplog is simply a server log, something that&#8217;s always been on the Eve roadmap. What makes it a little bit different is its ability to be exposed as a read-only API endpoint. This would in turn allow clients to query it as they would with any other standard endpoint. <!--more-->

Every oplog entry contains few important informations about the document
  
involved with the edit operation:

  * URL of the endpoint hit by the operation.
  * Kind of operation performed.
  * Unique ID of the document.
  * Date when the document was updated.
  * Date when the document as created.
  * User token, if [User Restricted Resource Access][3] is enabled for the endpoint

Like any other API-maintained documents, oplog entries also contain:

  * Unique ID
  * ETag
  * [HATEOAS][4] meta fields, if enabled.

A typical oplog entry would look something like this:

    {
        "o": "DELETE", 
        "r": "people", 
        "i": "542d118938345b614ea75b3c",
        "_updated": "Fri, 03 Oct 2014 08:16:52 GMT", 
        "_created": "Fri, 03 Oct 2014 08:16:52 GMT",
        "_id": "542e5b7438345b6dadf95ba5", 
        "_etag": "e17218fbca41cb0ee6a5a5933fb9ee4f4ca7e5d6"
        "_links": {...},
    }
    

To save a little storing space field names have been shortened when possible (what can I say, I&#8217;m a MongoDB guy): `o` stands for operation, `r` stands for resource, `i` stands for unique ID and `c` stands for changes. Other keys are defined by the configuration settings, and their default names are shown here.

## How is the oplog operated?

Three new settings keywords are available:

  * `OPLOG`
  
    Sets the oplog name and defaults to `oplog`. This is the name of the collection on the database and also the default url for the oplog endpoint.</p> 
  * `OPLOG_METHODS`
  
    A list of HTTP methods for which oplog entries are to be recorded. Defaults to `['DELETE']`.</p> 
  * `OPLOG_ENDPOINT`
  
    Set it to `True` if an oplog endpoint should be made available by the API. Defaults to `False`.

  * `OPLOG_AUDIT`
  
    If enabled, IP addresses and changes introduced with `PATCH` and `PUT` methods are also logged. Defaults to `True`.

So by default the oplog is stored on a conveniently named `oplog` collection, it only stores informations about deleted documents.

Since the eventual oplog endpoint is a standard API endpoint, if it is enabled the API maintainer can also fiddle with the endpoint settings as he/she would do with any other Eve endpoint. This allows for setting custom authentication (you probably want this resource to be only accessible for administrative purposes), changing the url, etc. Just add an `oplog` entry to the [API domain][5], like so:

    'oplog': {
        'url': 'log',
        'auth': my_custom_auth_class,
        'datasource': {'source': 'myapilog'}
    }
    

Note that while you can change most settings, the endpoint will always be read-only, so setting either `resource_methods` or `item_methods` to something else than `['GET']` will serve no purpose. Also, unless you need to do so, adding an oplog entry to the API domain is not required as it will be added automatically for you.

## Why the OpLog?

Clients have always been able to retrieve changes by simply querying an endpoint with a `If-Modified-Since` request. So why do we need an operations log? Of course because server-side logging is cool, and so is auditing, but it&#8217;s not only about that.

### Single entry point for all API updates

From the client perspective and for most use cases logging inserted, edited and replaced documents is probably a waste of both space and time, and this is the main reason why only `DELETE` operations are logged by default. However, I believe there are scenarios where remote access to a full activity log can be useful.

Imagine an API which is accessed by multiple apps (say phone, tablet, web and desktop applications) and all of them need to stay in sync with each other and the server. Instead of hitting every single endpoint with a `IMS` request they could just access the oplog. That&#8217;s a single request vs several, and since the oplog itself is a standard API endpoint, they could also perform `IMS` requests against it for optimal gains:

> Server, please send me all the changes occurred to the API since my last access. Sincerely, Your Client. 

Again this is not always the best approach a client could take. Sometimes it is probably better to only query for changes when they are really needed, but it seems cool to have both approaches available (and remember, the oplog endpoint is disabled by default).

### Fixing 304s

And then there are deleted documents which are a completely different beast. With no oplog we would have no way to tell if and when any document has been deleted, let alone inform clients about that. Actually, there is an [open ticket][6] precisely about this, and it&#8217;s been sitting there for a while.

When a `If-Modified-Since` request is received, the API is expected to respond with a `304 Not Modified` status if no changes occurred, so that clients can conveniently fallback to cached data. Up to version 0.4 (the official release at the time of this writing) Eve has been doing exactly that, with one caveat: missing documents were being ignored as, in the contest of the `IMS` request, there was no way to know about them.

The operations log will allow Eve powered APIs to take deleted documents into account, returning perfectly proper `304` codes as needed. The impact on performance should be minimal as we will only query the oplog when and if no changes have been detected on the target collection.

This solves only one half of the problem however. What happens when a `IMS` request comes in and deleted documents are found in the backlog? How do we report them back to the client? Three options come to mind which would address this scenario:

  1. Respond with a `200 OK` and a the usual &#8220;changes since `IMS` date&#8221; payload, which might happen to be empty if only deletions occurred in the time window. The client can then go and query the oplog endpoint with the same `IMS` date, finally getting the list of deleted documents IDs. 
  2. Include deleted documents IDs in the standard payload (within the `_items` list), maybe with a `deleted` status tag. This status tag is something new though, and for consistency we should probably add it to other objects in the payload.

  3. Add support for a new `_deleted` meta field in resource payloads. When deleted documents are spotted in the backlog the response payload will include them in their own list. Something like this:

<pre><code class="python">{
    "_items": [&lt;list of edited and added documents&gt;],
    "_deleted": [&lt;list of deleted document IDs&gt;]
    ...
}
</code></pre>

First option is so bad I should probably not be listing it at all. It would take two roundtrips to get the whole update down. Also, it would kind of force API maintainers to open the oplog endpoint to their clients.

I&#8217;m not convinced #2 would be a good idea either, as objects in the items list would not be homogeneous anymore and we would have to add support for a new meta field anyway (the status tag).

Option #3 on the other hand looks quite good to me. It does not require multiple requests to handle the case of deleted documents on `IMS` requests, and it is still easy and clean for clients to process. I am going to go with #3 unless feedback is negative and for good reasons, so let your opinion be heard.

## Closing concerns

I am slightly concerned about the performance impact, not so much on `IMS` requests but rather on write operations, especially when a complete, all-operations log is being recorded.

In MongoDB world OpLog is probably an ideal candidate for a [capped collection][7]. I&#8217;m not entirely convinced about that though, as by its nature a capped collection is bound to lose data over time, which again might lead to inaccurate `304` handling.

I am not implementing the OpLog at the data layer level however. It is a business layer feature to let other engines take advantage of it. Nothing prevents the MongoDB admin from setting the `oplog` as a capped collection anyway. Also, keep in mind that like all other resources maintained by the API, indexes are not handled by Eve itself so you will have to do your homework in that field too.

So here you have it. I&#8217;m currently done on both configuration and logging parts and will be working on `304` handling and response payloads in the coming days so that all of this can be included with next version 0.5. Be warned that at the moment the `develop` branch has no support for `IMS` requests on resource endpoints. It&#8217;s been disabled to avoid providing clients with inaccurate responses (see the ticket above).

If you have any comment or feedback to provide, please let me know in the comments below. I&#8217;d really appreciate that.

PS. In case you are wondering yes, the Eve OpLog is heavily inspired by the awesome [MongoDB OpLog][8].

 [1]: http://python-eve.org
 [2]: https://github.com/nicolaiarocci/eve/tree/oplog
 [3]: http://python-eve.org/authentication.html#user-restricted-resource-access
 [4]: http://python-eve.org/features.html#hateoas
 [5]: http://python-eve.org/config#domain-configuration
 [6]: https://github.com/nicolaiarocci/eve/issues/334
 [7]: http://docs.mongodb.org/manual/core/capped-collections/
 [8]: http://docs.mongodb.org/manual/core/replica-set-oplog/
