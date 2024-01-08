---
title: 'How to: Add custom JeSuisCharlie header to API responses'
author: Nicola Iarocci
date: 2015-01-12
url: /how-to-add-a-je-suis-charlie-header-to-api-responses/
categories:
  - Programming
tags:
  - eve
  - jesuischarlie
  - python
---
A lot of servers have been including a `JeSuisCharlie` header with their responses. If you haven&#8217;t already, try with Charlie Hebdo site itself:

    $ curl -I charliehebdo.fr
    Date: Mon, 12 Jan 2015 15:56:13 GMT
    Content-Type: text/html; charset=iso-8859-1
    Content-Length: 221
    Connection: keep-alive
    Location: http://www.charliehebdo.fr/index.html
    Vary: Accept-Encoding
    X-Charlie-fr: Je suis toujours Charlie.
    X-Charlie-en: I am still Charlie.
    X-Charlie-es: Todavia soy Charlie.
    X-Charlie-de: Ich bin immer Charlie.
    X-Charlie-ro: Inca sunt Charlie.
    X-Charlie-cz: Jsem stale Charlie.
    

I find this to be a great way for us techies to somehow contribute and show support for the ongoing anti-terrorism campaign. So if you feel like doing it here is a quick rundown on how to serve custom headers with your Eve-powered REST API. It is actually a very easy task to accomplish.

Eve provides [its own set][1] of callback hooks but since we don&#8217;t need fine-grained control (we are good with including the new header with all responses), this time we will leverage Flask&#8217;s [native][2] callback system instead.

    @app.after_request
    def after_request(response):
        response.headers.add('X-Charlie', 'Je Suis Charlie.')
        response.headers.add('X-Ahmed', 'Je Suis Ahmed.')
        return response
    

A simple run script would then look something like:

    from eve import Eve
    app = Eve()
    
    @app.after_request
    def after_request(response):
        response.headers.add('X-Charlie', 'Je Suis Charlie.')
        response.headers.add('X-Ahmed', 'Je Suis Ahmed.')
        return response
    
    if __name__ == '__main__':
        app.run()
    

All API responses now include the custom headers:

    $ curl http://localhost:5000
    HTTP/1.0 200 OK
    Content-Type: application/json
    Content-Length: 141
    Server: Eve/0.5 Werkzeug/0.9.6 Python/2.7.8
    Date: Mon, 12 Jan 2015 15:39:36 GMT
    X-Charlie: Je Suis Charlie.
    X-Ahmed: Je Suis Ahmed.
    

If you want to see it in action try sending a GET request with `curl`, `Postman` or similar tool to the Eve [demo instance][3] ([source][4]). Remember Eve is a Flask subclass so whatever works with Flask generally works with Eve too.

If you want to get in touch, I am [@nicolaiarocci][5] on Twitter.

 [1]: http://python-eve.org/features.html#event-hooks
 [2]: http://flask.pocoo.org/snippets/53/
 [3]: http://eve-demo.herokuapp.com/
 [4]: https://github.com/nicolaiarocci/eve-demo/blob/master/run.py
 [5]: http://twitter.com/nicolaiarocci
