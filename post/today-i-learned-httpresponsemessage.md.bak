---
date: 2020-12-04T07:05:25+01:00
title: "HttpResponseMessage.Content is non-nullable in NET5"
description: Today I learned the hard way that NET5 changed the HttpResponseMessage.Content type from nullable to non-nullable
share: false
---

Today I was happily migrating some C# projects to Net 5 when I stumbled upon
something unexpected. My focus was on a library (a NetStandard2.0 REST API
client, an SDK) and its associated test suite. The test project was a NetCore
3.1 application.

As you can imagine, being a REST API client, the library does a lot of talking
with a remote Web Service. It does that by leveraging the almightly
`System.Net.HttpClient.` The library has a private, static
`HttpResponseMessage` parser method. Its job is, well, to parse all responses
from the remote. It looks for known, expected headers, gracefully handle them,
and then deserializes the response content, if there is any.

The test suite has one primary task: to ensure that the SDK can adequately
handle the request-response cycle. It does that by mocking
a `HttpMessageHandler,` which is then used by the library HttpClient on every
test run. 

Until this morning, all 239 tests were passing just fine. Then, I switched the
test project's target framework moniker (TFM) to `net5.0`. Suddenly, most tests
went red. 

With no code changes, only a rebuild after the TFM switch, I knew I was up
to something weird.  

A couple of debug breakpoints later, I was back looking at my little response
parser, contemplating the following, rather innocent-looking line:

    if (httpResponseMessage.Content == null) return (response, token);

Its purpose is to skip deserialization if there no content in the response.
I knew all the failing tests had no response content. 

When the caller (the test suite in this case) is a NetCore 3.1 application, it
passes a `HttpResponseMessage` whose `Content` value is null, as expected.
Instead, it appears that when a NET5 application invokes the same method, the
`HttpResponseMessage.Content` carries an obscure `EmtpyContent` value.
Unexpected and, more importantly, undocumented (at least to my knowledge[^1].)

A not-so-quick investigation revealed that, in fact, sometime during the NET5
development process, the type of `HttpResponseMessage.Content` has changed from
nullable to non-nullable[^2]. 

    if (httpResponseMessage.Content == null || 
        httpResponseMessage.Content.Headers.ContentLength == 0)
        return response;

The double condition makes sure that no matter the calling moniker, we'll
handle it just fine. 

There we go. All tests are green again.

*Enjoyed this post? Subscribe to the [newsletter][nl] or follow @[nicolaiarocci][tw] on Twitter.*

 [^1]: [Breaking changes in .NET 5.0](https://docs.microsoft.com/en-us/dotnet/core/compatibility/5.0)
 [^2]: [Make HttpResponseMessage.Content non-nullable](https://github.com/dotnet/runtime/pull/35910)

 [tw]: http://twitter.com/nicolaiarocci
 [nl]: http://eepurl.com/b-_Pzz

