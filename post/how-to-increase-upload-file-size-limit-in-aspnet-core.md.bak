---
date: 2021-02-26T07:05:25+01:00
title: "How to increase upload file size in ASP.NET Core"
share: false
tags: ["til", "aspnetcore", ".net"]
---
Today I learned the hard way that since ASP.NET Core 2.0, the request body has
acquired a default size limit at 30MB (~28.6 MiB).

> If the request body size exceeds the configured max request body size limit,
> the call to Request.Body.ReadAsync will throw an IOException. If this
> exception is uncaught, Kestrel will respond with a 413 Payload Too Large
> response and HttpSys will respond with a generic 500 Internal Server Error
> response ([source][1]).

This will be a breaking change if your endpoint is expected to handle large
uploads. The solution is simple, just decorate your MVC action or controller
with the `RequestSizeLimit` attribute, like so:

```
    [HttpPost]
    [RequestSizeLimit(100_000_000)]
    public IActionResult MyAction([FromBody] MyViewModel data)
    {
```

`DisableRequestSizeLimit` can be used to make request size unlimited. This
effectively restores pre-2.0.0 behavior for just the attributed action or
controller. You can also change or disable the limit programmatically, either
on a per-request basis or globally (see the instructions at this [link][1].) 

In my case, however, disabling the request limit was not enough. Because my
endpoint is expecting an `IFormFile` argument, I also had to set the
`RequestFormLimits` attribute:

```
    [HttpPost]
    [DisableRequestSizeLimit,
    RequestFormLimits(MultipartBodyLengthLimit = int.MaxValue, 
        ValueLengthLimit = int.MaxValue)]
    public async Task<ActionResult> BulkAdd(string schema, IFormFile file)
    {
```

Please note that all of this happened on a .NET 5 Linux application with
Kestrel running behind nginx. As pointed out at the link above, if you're
running behind IIS, then the limit is disabled, and the usual *web.config*
limit applies.

For future reference, [here][2] are the current Kestrel limits.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://github.com/aspnet/Announcements/issues/267
 [2]: https://github.com/dotnet/aspnetcore/blob/main/src/Servers/Kestrel/Core/src/KestrelServerLimits.cs
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
