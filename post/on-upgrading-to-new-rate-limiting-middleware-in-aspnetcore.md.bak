---
date: 2022-12-23T07:05:25+01:00
title: "On implementing the ASP.NET Core 7 rate-limiting middleware"
share: false
tags: ["dotnet", "rate-limiting", "programming", "til"]
---
Today, my last self-assigned duty before the Christmas break was to migrate
our in-house rate-limiting implementation (based on the
[AspNetCoreRateLimiting][1] third-party package) to the new, shiny
[rate-limiting middleware][2] introduced by ASP.NET Core 7. While the process
was relatively straightforward, I stumbled upon a few quirks I want to annotate
here.

Our use case is simple. We use what the ASP.NET Core 7 documentation defines as
a "fixed window limiter." It uses a specified time window to limit requests.
When the time window expires, a new time window starts, and the request limit
is reset. Consider the following code (for convenience, I'm using an extension
method):

```
public static void ConfigureRateLimit(this IServiceCollection services)
{
    services.AddRateLimiter(x => 
        x.AddFixedWindowLimiter(
                policyName: "fixed", options =>
                {
                    options.PermitLimit 1;
                    options.Window = TimeSpan.FromSeconds(10);
                    options.QueueLimit 1;
                }));
}
```

It sets a window of 10 seconds. Within that window, a maximum of one request is
allowed. Exceeding requests will be queued and served at window reset. Notice
that we defined "fixed" as the policy name. 

Once our policy is configured, we must instrument the app instance to use the
rate limiter, then we call `RequireRateLimiting` on our endpoints:

```
app.UseRouting();  // I'm mentioning this line for good reason, see below
app.UseRateLimiter();
app.UseEndpoints(endpoints => { endpoints.MapControllers()
    .RequireRateLimiting("fixed"); });
```

Nothing else is needed, really, for such a simple scenario. We could be more
sophisticated. We could opt for more advanced options, like a "sliding windows
limiter" or a "bucket token limiter"; we could apply rate limiting only to
specific endpoints or controllers or mix and match these options. I chose to
ditch hard-coded settings and read them from the configuration file. My
*appsettings.json* contains the following (with different vaues):

```
  "RateLimiter": {
    "PermitLimit": 1
    "Window": 10,
    "QueueLimit": 1
  }

```

The `RateLimiter` class maps the json structure:

```
public class RateLimiter
{
    public int PermitLimit { get; set; }
    public int Window { get; set; }
    public int QueueLimit { get; set; }
}
```
The updated code looks like this:

```
public static void ConfigureRateLimit(this IServiceCollection services, 
    IConfiguration configuration)
{
    var rateLimiter = new RateLimiter();
    configuration.GetSection("RateLimiter").Bind(rateLimiter);
    
    services.AddRateLimiter(x => 
        x.AddFixedWindowLimiter(
                policyName: "fixed", options =>
                {
                    options.PermitLimit = rateLimiter.PermitLimit;
                    options.Window = TimeSpan.FromSeconds(rateLimiter.Window);
                    options.QueueLimit = rateLimiter.QueueLimit;
                }));
}
```


I wish I could say it all worked splendidly on the first try. The API was
running fine, but it was not rate-limited. It looked like the middleware was
not being invoked, or it somehow failed miserably and silently. After an
embarrassingly long time, I figured out the problem: `UseRateLimiter`
*must* be called after `UseRouting`. 

Before:

```
app.UseRateLimiter();
app.UseRouting();
app.UseEndpoints(endpoints => { endpoints
    .MapControllers().RequireRateLimiting("fixed"); });
```

After:

```
app.UseRouting();
app.UseRateLimiter();
app.UseEndpoints(endpoints => { endpoints.MapControllers()
    .RequireRateLimiting("fixed"); });
```

Simply switching two lines saved the day. I looked high and low but could not
find any reference to this requirement. If intended, it should be mentioned in
the documentation. If it is a bug, it should be fixed (and I should
probably open at ticket about it.)


Anyways, now the API is rate-limited via the new middleware. The first request
sent via Postman goes through. The second, rapid-fired one is queued and served
at window reset, as expected. A third request within the same window is bounced
back. 

However:

1. You get a `503 Service Unavailable` response. I'm not in favor of 500
   replies for this case. Five-hundreds should be reserved for server errors,
   and that's not what we are dealing with here. My previous implementation
   served a more appropriate `429 Too Many Requests`.
2. No `Retry-After` header is included with the response. I think it's
   mandatory to instruct clients on what to do next.

Luckily, the rate-limiting middleware allows for ample customization. On
defining our policy, we can attach a custom function to the `OnRejected` event.
The code below is updated to address both issues above:

```
public static class ServicesConfiguration
{
    public static void ConfigureRateLimit(this IServiceCollection services, 
        IConfiguration configuration) {

        var rateLimiter = new RateLimiter();
        configuration.GetSection("RateLimiter").Bind(rateLimiter);
        
        services.AddRateLimiter(x => 
            x.AddFixedWindowLimiter(
                    policyName: "fixed", options => {
                        options.PermitLimit = rateLimiter.PermitLimit;
                        options.Window = TimeSpan.FromSeconds(rateLimiter.Window);
                        options.QueueLimit = rateLimiter.QueueLimit;
                    })

                // new code here:
                .OnRejected = (context, _) => {

                // inject Retry-After header (too much line wrapping, I know)
                if (context.Lease.TryGetMetadata(MetadataName.RetryAfter, 
                    out var retryAfter)) {
                    context.HttpContext.Response.Headers.RetryAfter =
                        ((int) retryAfter.TotalSeconds).ToString();
                }
                // return a different status code
                context.HttpContext.Response.StatusCode = 
                    StatusCodes.Status429TooManyRequests;
                return new();
            });
    }
```

And that's all there is to it. I dropped the AspNetCoreRateLimiting dependency.
That is one great piece of software, and I am grateful to its author Stefan
Prodan and his contributors. As mentioned in [My Top 7 New Features in .NET
7][3], they recently released a package that allows using Redis as a
rate-limiting backend. I might adopt it in the future. 

Complete documentation for ASP.NET Core 7 rate-limiting middleware is available
[here][4].


*Subscribe to the [newsletter][nl], the [RSS feed][rss], or [follow me on Mastodon][m]*

 [1]: https://github.com/stefanprodan/AspNetCoreRateLimit
 [2]: https://devblogs.microsoft.com/dotnet/announcing-rate-limiting-for-dotnet/
 [3]: /my-top-7-new-features-in-.net-7/
 [4]: https://learn.microsoft.com/en-us/aspnet/core/performance/rate-limit?view=aspnetcore-7.0
 [rss]: https://nicolaiarocci.com/index.xml
 [m]: https://fosstodon.org/@nicola
 [nl]: https://buttondown.email/nicolaiarocci
