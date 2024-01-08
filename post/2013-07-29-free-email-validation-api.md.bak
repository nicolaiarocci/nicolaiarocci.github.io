---
title: Free Robust Email Validation API
author: Nicola Iarocci
date: 2013-07-29
url: /free-email-validation-api/
dsq_thread_id:
  - 2024957168
categories:
  - Programming
tags:
  - api
  - email validation
---
The guys at Mailgun are taking a <a href="http://blog.mailgun.com/post/free-email-validation-api-for-web-forms/" target="_blank">very interesting approach</a> at the ever-lasting problem of proper Email validation:

> Given an arbitrary address this service validates address based off syntax checks (RFC defined grammar), DNS validation, spell checks, and if available, Email ServiceProvider (ESP) specific local-part grammar.

They&#8217;re relying on <a href="https://en.wikipedia.org/wiki/Parsing" target="_blank">formal grammar</a> and not on regex like the rest of us, which is perhaps the more intriguing aspect of the project. Being Email Service Providers themselves they have good knowledge of most ESPs local-part grammars (the left side of the @ symbol) so when there is a match, they&#8217;re validating local-parts too.

At the cost of a slight delay DNS, MX and A record validation adds robustness to the process (didn&#8217;t really perceive any slowness during my tests). What really shines however, at least in my eyes, is the included &#8220;correct address suggestion service&#8221;.

At the moment they are providing a <a href="https://api.mailgun.net/v2/address" target="_blank">free API</a>  and a <a href="http://mailgun.github.io/validator-demo/" target="_blank">mail address validation page</a>. Here&#8217;s the catch: consuming the API requires a free Mailgun account. According to their own statement however they are also going to [open source the tool][1] and yes, it&#8217;s going to be in Python.

 [1]: http://blog.mailgun.com/post/free-email-validation-api-for-web-forms/#comment-977817227
