---
date: 2022-02-27T07:05:25+01:00
title: "Parameter null-checking added to C# 11 Preview"
url: "paramter-null-checking-added-to-csharp-11-preview"
share: false
tags: ["csharp", "dotnet"]
---
The [first preview][1] of C# 11 is out, and well, I think I like what I see.
I dig the new [List patterns][2] and am a fan of [allowing newlines in the
"holes" of interpolated strings][3]. [Parameter null-checking][4] is a bit
contentious, and it's good that they are releasing it in preview one and asking
for feedback.

In a nutshell, they want to spare us a lot of boilerplate. Code like this:

    public static void M(string s)
    {
        if (s is null)
        {
            throw new ArgumentNullException(nameof(s));
        }
        // Body of the method
    }


Would be abbreviated by adding `!!` to the parameter name:

    public static void M(string s!!)
    {
        // Body of the method
    }

> Code will be generated to perform the null check. The generated null check
> will execute before any of the code within the method. For constructors, the
> null check occurs before field initialization, calls to base constructors,
> and calls to this constructors.

My initial reaction was, we don't need this; we got Nullable Reference Types.
NRTs however help at design time, to know whether a null is possible, while
parameter null-checking is meant for runtime. 

According to Kathleen Dollard, the .NET Runtime itself removed nearly 20,000
lines of code using this new null-check syntax. That's one heck of a lot of
boilerplate removed. 

I don't think I like the syntax, though. It's super concise, which is good, and
I appreciate putting the `!!` on the parameter rather than the type since
the parameter's value is being checked. Still, the two-punctuation character
seems a bit clumsy. Someone suggested adopting `notnull` instead:

    public void M(string s notnull) { // code }

I like this suggestion. I wouldn't want `notnull` on the left of the parameter
name. To the right? Count me in.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://devblogs.microsoft.com/dotnet/early-peek-at-csharp-11-features/
 [2]: https://devblogs.microsoft.com/dotnet/early-peek-at-csharp-11-features/#c-11-preview-list-patterns
 [3]: https://devblogs.microsoft.com/dotnet/early-peek-at-csharp-11-features/#c-11-preview-allow-newlines-in-the-holes-of-interpolated-strings
 [4]: https://devblogs.microsoft.com/dotnet/early-peek-at-csharp-11-features/#c-11-preview-parameter-null-checking
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
