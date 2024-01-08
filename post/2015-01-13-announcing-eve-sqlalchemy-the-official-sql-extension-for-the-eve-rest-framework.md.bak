---
title: Announcing Eve-SQLAlchemy the official SQL extension for the Eve REST Framework
author: Nicola Iarocci
date: 2015-01-13
url: /announcing-eve-sqlalchemy-the-official-sql-extension-for-the-eve-rest-framework/
categories:
  - Programming
tags:
  - eve
  - python
  - sql
---
Powered by SQLAlchemy and good intentions, [Eve-SQLAlchemy][1] is an official [Eve][2] extension which allows to effortlessly build and deploy highly customizable, fully featured RESTful Web Services with SQL backends.

As with all Eve extensions, once installed with

    $ pip install eve-sqlalchemy
    

using Eve-SQLAlchemy is very simple:

    from eve import Eve
    from eve_sqlalchemy import SQL
    
    app = Eve(data=SQL)
    app.run()
    

On a fresh virtualenv (of course you are using virtualenvs, right?) the install will also setup Eve and all its dependencies for you. For a complete tutorial you can visit the Eve-SQLAlchemy [Support Website][3].

If you have been following the Eve development you probably know that the original plan was to release SQL support within the Eve core, alongside with the native MongoDB layer. In fact, in a [long rant][4] on open source and code responsibility I took the chance to outline the path forward.

However, if you check the discussion which spread in the comments below that post you can see how both my friend and fellow MongoDB Master [Flavio][5] and the main contributor to the sqlalchemy branch [Andrew][6] were suggesting that a plugin system for data layers might be more appropriate. Not coincidentally that was easy to accomplish since the Eve data layer system was designed precisely with that goal in mind, right from the start.

So, to make a long story short, in agreement with Andrew who volountereed for the task, we changed plans. He refactored the sqlalchemy branch into a separate repository&#8230; and then the official Eve SQL extension was born. This approach also allows the extension and Eve to develop asynchronously which is ideal for a faster release cycle.

I like this setup so much that, if in time it shows to be as good as I think it will be, I will probably want to experiment with taking the MongoDB layer out of Eve core too. So with Eve 0.6 MongoDB support would still be preinstalled along with core (so nothing changes as first time user experience) but, being a separate package, users could easily switch to a different driver as they need, still keeping their Eve setup as light as possible.

So if you are willing to help with the development of a mature SQL driver please feel free to join Andrew and other contributors. Your help is more than welcome. Allow me thank them all individually, for the work they&#8217;ve been doing on the SQL code is absolutely amazing: Andrew Mleczko, Tomasz Jezierski (Tefnet), Bruce Frederiksen, Jacopo Sabbatini and Peter Zinng.

Get [Eve-SQLAlchemy v0.1][7] while it&#8217;s hot!

If you want to get in touch, I am [@nicolaiarocci][8] on Twitter.

 [1]: https://github.com/RedTurtle/eve-sqlalchemy
 [2]: http://python-eve.org
 [3]: http://eve-sqlalchemy.readthedocs.org/
 [4]: http://nicolaiarocci.com/open-source-and-code-responsibility/
 [5]: http://www.flaper87.com/
 [6]: https://github.com/amleczko
 [7]: https://pypi.python.org/pypi/Eve-SQLAlchemy/0.1
 [8]: http://twitter.com/nicolaiarocci
