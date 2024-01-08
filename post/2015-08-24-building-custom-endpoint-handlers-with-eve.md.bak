---
title: Custom endpoint handlers with Eve
author: Nicola Iarocci
date: 2015-08-24
url: /building-custom-endpoint-handlers-with-eve/
dsq_thread_id:
  - 4062301697
categories:
  - Programming
tags:
  - eve
  - python
---
On [Stack Overflow][1] and the Eve [mailing list][2], but also in my mailbox and even on Twitter, I get a lot of enquiries on how to build custom endpoints within a Eve-powered RESTful application. Now, since within Eve all endpoints are fully customizable, what they really mean is:

> How do I setup endpoints without any binding to a data entity, just connected to a custom method? 

They would like to call something like `/mycustomendpoint` and get the response from a method they have defined somewhere in the Python sources. The standard endpoint-entity mapping provided by Eve covers 90% of their needs, but sometimes they just need endpoints that have nothing to do with data entities.

This is very easy to achieve. I&#8217;m writing it down so I can point people to this post in the future.

## Eve _is_ Flask

[Eve][3] is a Flask application and I really mean it since it is, in fact, a Flask subclass. Eve adds out-of-the-box [RESTful capabilities][4] to the Flask micro-framework. Most of the time you will be happy with just Eve&#8217;s own features but remember, the full [Flask][5] (and [Werkzeug][6] at a lower level) features set is also part of your arsenal.

> Whatever you can do with Flask, you can do with Eve

So yes, of course you can easily set some functions to be invoked when a custom endpoint is hit with a request. The following snippet is a slightly modified version of Flask&#8217;s very own [Quickstart][7] tutorial:

{{< gist nicolaiarocci 01ea2cd1068afc99f9e38f0bb9afcabf >}}

By decorating the `hello_world` method with the `route` decorator we added a new endpoint to the application. Each time a request to `/hello` comes in, it will be routed to our custom method. Of course the regular API endpoints (either defined in `settings.py`, passed as a dict at launch, or registered live by calling the `register_resource` method) will also be available.

If you have an [Eve authentication class][8] securing regular API endpoints, you can apply it to your custom endpoint too. Just add a `requires_auth` decorator:

{{< gist nicolaiarocci 3fc0379e083266f20faf12b209108aa9 >}}

Say that you saved the above snippet as _run.py_ and also have your RESTful endpoints properly [configured][9]. Launch the script:

{{< gist nicolaiarocci 697f85ee10b7e0c0b601fdd21b171a15 >}}

You can now point your browser to `http://localhost:5000/hello/` and enjoy the application greeting. Or you can consume any other configured API endpoint.

As all of Flask features are at your fingertips you might as well opt for registering a [blueprint][10], which is what the awesome [Eve-Docs][11] extension is doing in order to provide a static HTML `/docs` endpoint on top of any Eve powered API.

 [1]: https://stackoverflow.com/questions/24134383/servicing-html-requests-with-eve/
 [2]: https://groups.google.com/forum/?hl=en#!topic/python-eve/LM9kZkgq3vA
 [3]: http://python-eve.org
 [4]: http://python-eve.org/features
 [5]: http://flask.pocoo.org
 [6]: http://werkzeug.pocoo.org
 [7]: http://flask.pocoo.org/docs/0.10/quickstart/#a-minimal-application
 [8]: http://python-eve.org/authentication.html
 [9]: http://python-eve.org/config
 [10]: http://flask.pocoo.org/docs/0.10/blueprints/
 [11]: https://github.com/charlesflynn/eve-docs
