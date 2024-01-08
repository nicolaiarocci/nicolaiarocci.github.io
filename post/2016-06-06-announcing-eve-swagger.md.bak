---
title: Meet Eve-Swagger the swagger.io extension for your Eve powered REST API
author: Nicola Iarocci
date: 2016-06-06
share: false
url: /announcing-eve-swagger/
categories:
  - Programming
tags:
  - eve
  - python
  - swagger
---
[Eve-Swagger][1] is a swagger.io extension for [Eve][2] powered RESTful APIs. It has been around for a while on GitHub but I never managed to officially release it. So rejoice! it is now available on PyPI.

But what is Swagger, and why is it useful to your RESTful API? With a Swagger-enabled API you can get interactive documentation, client SDK generation and discoverability, all for free. From [Swagger website][3]:

> Swagger is a simple yet powerful representation of your RESTful API. With the largest ecosystem of API tooling on the planet, thousands of developers are supporting Swagger in almost every modern programming language and deployment environment. With a Swagger-enabled API, you get interactive documentation, client SDK generation and discoverability. 

When Eve-Swagger is installed and properly configured your Eve API exposes
a special `/api-docs` endpoint which returns a 100% swagger-compliant JSON
response. This JSON can then be processed by the swagger tools like [Swagger
UI][4] and [Swagger Editor][5]. Here we can appreciate Swagger UI providing API
documentation out of the box (click to zoom):

![Swagger UI](/images/Screen-Shot-2016-06-06-at-15.13.04.png)

Like most Eve extensions Eve-Swagger comes as a standard Flask Blueprint and, as such, using it is very simple:

{{< gist nicolaiarocci 7720dd28f2e74e77c94edcb487aa5102 >}}

Once the blueprint has been registered all you have to do is add a `SWAGGER_INFO` node to your settings. It maps to a swagger [infoObject][6] and contains some simple, human readable information. The extension will also scan your endpoint settings to figure out the API graph and document it. Of course, in order to not to clutter your launch script, you could (and probably should) set `SWAGGER_INFO` in your [configuration file][7].

Installation is super easy:

{{< gist nicolaiarocci a7d2e3d8451f13907de6347448346c00 >}}

This is just version 0.0.2 so many parts might still be moving, but you are encouraged to start using it right away. Also if you appreciate this extension please let me know by either starring it on GitHub or with a tweet or email, so I will know that I should really try hard and allocate more time to this project. As always, feel free to contribute via pull request!

If you want to get in touch, I am [@nicolaiarocci][8] on Twitter.

 [1]: https://github.com/nicolaiarocci/eve-swagger
 [2]: http://python-eve.org
 [3]: http://swagger.io
 [4]: https://github.com/swagger-api/swagger-ui
 [5]: http://editor.swagger.io/#/
 [6]: http://swagger.io/specification/#infoObject
 [7]: http://python-eve.org/config
 [8]: https://twitter.com/nicolaiarocci
