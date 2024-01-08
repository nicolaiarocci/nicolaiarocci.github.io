---
date: 2023-11-09T07:05:25+01:00
title: "How to use XmlWriter along with StringWriter to properly serialize a UTF-8 string"
share: false
tags: ["til", "dotnet", "programming", "csharp"]
---
Today, I (re)learned how to serialize an XML to a UTF-8 string. Like all the other times I did this, I got backstabbed
by StringWriter, which only supports UTF-16. A simple code snippet like this:

```
    await using var sw = new StringWriter();
    await using var w = XmlWriter.Create(sw, new() { Async = true });
    ...
    await w.FlushAsync();
    return sw.ToString();
```

Will emit this output:

```
    <?xml version="1.0" encoding="utf-16"?><...
```

There's nothing inherently wrong with UTF-16, but XML is usually UTF-8, so one must do something about it. StringWriter
exposes an `Encoding` property, but it is read-only for unknown reasons. One might think that given that the XmlWriter
allows setting its own `Encoding` value, something like this would work:

```
    await using var sw = new StringWriter();
    await using var w = XmlWriter.Create(sw, 
        new() { Async = true , Encoding = Encoding.UTF8});
    ...
    await w.FlushAsync();
    return sw.ToString();
```

But it doesn’t. Over time, I’ve seen a few different ways to get out of this dead end, some more performant and or less
verbose than others, but my favorite is resorting to a custom StringWriter:

```
    public class Utf8StringWriter : StringWriter
    {
        public override Encoding Encoding => Encoding.UTF8;
    }
```

Armed with this, it is trivial, as it should have been from the get-go, to obtain the desired output:

```
    await using var sw = new Utf8StringWriter();
    await using var w = XmlWriter.Create(sw, new() { Async = true });
    ...
    await w.FlushAsync();
    return sw.ToString();

    // returns  <?xml version="1.0" encoding="utf-8"?><...

```

The whole .NET framework has seen fantastic performance improvements, top-class multi-platform support, and remarkable
streamlining, but some baffling pitfalls are still hidden in some of its less obvious parts. StringWriter not supporting
UTF-8 out-of-the-box is one of them.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or [follow me on Mastodon][m]*

 [rss]: https://nicolaiarocci.com/index.xml
 [m]: https://fosstodon.org/@nicola
 [nl]: https://buttondown.email/nicolaiarocci
