---
date: 2021-05-04T07:05:25+01:00
title: "dotnet SmtpClient should not be used"
share: false
tags: ["til", "dotnet", "programming"]
---
I am very late to the party, but today I learned that the good old dotnet
`SmptClient` is considered obsolete and should not be used. Quoting the
documentation:

> We don't recommend using the SmtpClient class for new development because
> SmtpClient doesn't support many modern protocols. Use MailKit or other
> libraries instead. ([source][1]) 

Interestingly, Microsoft is recommending a third-party open-source library as an
alternative. I hope we'll see more of that in the future. 

I just finished integrating [MailKit][2] in our backend. I must say that I'm
pleasantly surprised by its rich feature-set and the elegant and
straightforward design, which makes getting on-board super easy. It's built on
top of the excellent MimeKit, after all, and authored by the very same author
Jeffrey Stedfast.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://docs.microsoft.com/en-us/dotnet/api/system.net.mail.smtpclient?view=net-5.0&viewFallbackFrom=netcore-5.0#remarks
 [2]: https://github.com/jstedfast/MailKit
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
