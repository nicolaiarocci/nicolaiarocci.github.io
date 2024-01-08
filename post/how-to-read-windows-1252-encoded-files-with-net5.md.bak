---
date: 2021-08-27T07:05:25+01:00
title: "How to read Windows-1252 encoded files with .NETCore and .NET5+"
share: false
tags: ["til", "dotnet", "programming"]
---
Another day, another lesson learned: modern .NET does not support the
Windows-1252 encoding out of the box. Today my colleague was happily porting
a legacy NET4+ app to NET6. As usual, the port was super-easy; it would compile
and run just fine, so he was surprised when the app crashed reading a few
specific XML files. That's when I was called in. A closer inspection revealed
a pattern: all those crashing files were Windows 1252-encoded (the rest, a vast
majority, were UTF-8.)

It turns out that under NETCore/NET5+, to read Windows-1252 encoded files, we
first need to take a dependency on `System.Text.Encoding.CodePages`:

    dotnet add package System.Text.Encoding.CodePages

Then, we register a `CodePagesEncodingProvider` instance from the package:

    Encoding.RegisterProvider(CodePagesEncodingProvider.Instance);

Finally, on creating the XmlReader instance, we can set the encoding. To do
that, we need to pass an `XmlParserContext` instance, which allows us to
specify custom encoding:

    # Create the parser context and set the encoding
    var context = new XmlParserContext(null, null, null, XmlSpace.None)
    context.Encoding = Encoding.GetEncoding(1252);

    # Use the custom parser when reading the Xml
    using (var r = XmlReader.Create(fileName, null, context))
    {
        ...
    }


And sure enough, all those troublesome XML files are no problem anymore. It
works on all platforms: Linux, macOS, and Windows.  That's a lot of tinkering
for a small task that required no effort in the past. However, it makes sense
as .NET is now cross-platform, and we want to reduce the app's footprint as
much as possible.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
