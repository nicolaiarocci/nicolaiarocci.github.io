---
title: How about a Sentinel for your Flask Application?
author: Nicola Iarocci
date: 2015-02-04
url: /a-sentinel-for-your-flask-applications/
categories:
  - Programming
tags:
  - eve
  - flask
  - oauth2
  - python
---
[Flask-Sentinel][1] is a OAuth2 Server implementation of the Resource Owner Password Credentials Grant pattern described in [Section 1.3.3 of RFC 6749][2]. It is powered by Flask-Oauthlib, Redis and MongoDB and is bundled as a Flask extension so it can be used to add OAuth2 capabilities to an existing application.

So what is the Resource Owner Password Credentials Grant pattern? According to the official RFC:

> The resource owner password credentials (i.e., username and password) can be used directly as an authorization grant to obtain an access token. The credentials should only be used when there is a high degree of trust between the resource owner and the client (e.g., the client is part of the device operating system or a highly privileged application). 

A typical use case would be when the remote API maintainer controls the client application. Say that you have a REST API being consumed by your own iOS, Android, WinPhone, desktop or web applications. Users register to your service by creating their accounts. Then, they consume the service using your applications.

> Even though this grant type requires direct client access to the resource owner credentials, the resource owner credentials are used for a single request and are exchanged for an access token. This grant type can eliminate the need for the client to store the resource owner credentials for future use, by exchanging the credentials with a long-lived access token or refresh token. 

So let&#8217;s get back at the proprietary client scenario. The user has just installed the application on his/her device. On first run he/she is asked to provide his/her username and password. These are sent to the OAuth2 server through a SSL/TLS encrypted channel. If the user is registered for the service and the client id, which has also been sent along with the user credentials, is recognised, then the server sends back a valid access token. Otherwise responds with a `401 Unhautorized`.

From now on the application will only be using the access token for all requests until, eventually, the token expires. If that happens, the cycle repeats. Please note that in this scenario the client does not need to (and probably should not) store the username and/or password on the local cache. The User Credentials pattern usually relies on long lived tokens so asking again for username and password is not a big deal (you could also opt for permanent, revokable tokens.)

Flask-Sentinel provides two endpoints: one for token creation which defaults to `/oauth/token` and is consumed by clients, and another for users and clients management, accessible at `/oauth/management`:

<img src="http://i2.wp.com/raw.githubusercontent.com/nicolaiarocci/flask-sentinel/master/static/console.png?w=525&#038;ssl=1" alt="API Management" data-recalc-dims="1" />
  
Note that the password is hashed and salted on the server, so no plain password is stored on either sides of the channel.

Only existing users and recognised clients will be provided an access token. A typical token request would be as follows:

    $ curl -k -X POST -d \
      "client_id=9qFbZD4udTzFVYo0u5UzkZX9iuzbdcJDRAquTfRk&
       grant_type=password&
       username=jonas&
       password=pass" \
       <api_url>/oauth/token
    

And the response would be like so:

    {
        "access_token": "NYODXSR8KalTPnWUib47t5E8Pi8mo4", 
        "token_type": "Bearer", 
        "refresh_token": "s6L6OPL2bnKSRSbgQM3g0wbFkJB4ML", 
        "scope": ""
    }
    

The client can now use the access token to access protected API endpoints:

    $ curl -k -H \
      "Authorization:Bearer NYODXSR8KalTPnWUib47t5E8Pi8mo4" \
      <api_url>/endpoint
    
    200 OK
    

There are a number of configuration options of course, for example you can change the url of token and management endpoints, set token expiration, setup database connection, stuff like that. Redis is used to store active access tokens, allows for optimal performance.

While you can use Flask-Sentinel to extend an existing API, you might want to instance it as a stand-alone Flask application to optimize for scalability. You would end up with a distributed network of three different (micro)services: the OAuth2 server, the resouces API with protected endpoints as needed, and the Redis instance bridging the two. Check out the [project page][1] on GitHub for details.

Of course Flask-Sentinel integrates seamlessly with any [Eve][3] powered REST API. Check out the [Eve-OAuth2][4] sample, a fork of the original Eve-Demo project with a couple protected endpoints and a static HTML page, also protected.

The project is very new and lacks a few little things, but I suspect it is already usable even at this stage. Enjoy!

If you want to get in touch, I am [@nicolaiarocci][5] on Twitter.

 [1]: https://github.com/nicolaiarocci/flask-sentinel
 [2]: http://tools.ietf.org/html/rfc6749#section-1.3.3
 [3]: http://python-eve.org
 [4]: https://github.com/nicolaiarocci/eve-oauth2
 [5]: http://twitter.com/nicolaiarocci
