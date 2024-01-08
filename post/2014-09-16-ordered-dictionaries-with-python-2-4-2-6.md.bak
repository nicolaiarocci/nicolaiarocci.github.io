---
title: Ordered Dictionaries with Python 2.4-2.6
author: Nicola Iarocci
date: 2014-09-16
url: /ordered-dictionaries-with-python-2-4-2-6/
dsq_thread_id:
  - 3022454351
categories:
  - Programming
tags:
  - python
---
[OrderedDict][1] is a super handy data structure.

> An OrderedDict is a dict that remembers the order that keys were first inserted. If a new entry overwrites an existing entry, the original insertion position is left unchanged. Deleting an entry and reinserting it will move it to the end. 

Problem is, this stuff is only available in the standard library since Python 2.7 while [my project][2] also needs to support Python 2.6. Fortunately there&#8217;s a back-port available and it is only a pip install away:

    # make OrderedDict available on Python 2.6-2.4
    $ pip install ordereddict
    

[ordereddict][3] is based on the awesome recipe by [Raymond Hettinger][4], works with Python 2.4-2.6 and, most importantly, is a drop-in replacement for OrderedDict.

However if you want your code to run seamlessly on all Pythons there&#8217;s still some work to be done. First of all you want to make sure that the appropriate OrderedDict is imported, either the standard library version (for Python 2.7 and above) or the back-port release. <!--more-->

This is easily accomplished, and in a very pythonic way:

    try:
        # try with the standard library
        from collections import OrderedDict
    except ImportError:
        # fallback to Python 2.6-2.4 back-port
        from ordereddict import OrderedDict
    

## Fixing setup.py

If you are shipping your code as a package then you also want to make sure that setup.py properly handles the different Python versions. Since setup.py itself is nothing but standard Python module, we can make it more dynamic by applying the same technique above.

    #!/usr/bin/env python
    from setuptools import setup, find_packages
    
    # your standard required modules
    install_requires = [
        'simplejson',
        'cerberus',
        'events',
        ...
    ]
    
    try:
        from collections import OrderedDict
    except ImportError:
        # add backport to list of required modules
        install_requires.append('ordereddict')
    
    setup(
        name='appname',
        version='0.1',
        packages=find_packages(),
        ...
        # no matter which Python, we're now good to go
        install_requires = install_requires,
        ...
    )
    

## Handling requirements.txt

When it comes to pip&#8217;s requirements.txt, what I think works best is to simply add a _diff file_ which targets old Python versions like so:

    # py26-requirements.txt
    # install from 'canonical' requirements.txt first (DRY)
    -r requirements.txt
    # add specific Python 2.6 dependencies
    ordereddict
    

A developer using Python 2.6 would then go with

    $ pip install -r py26-requirements.txt
    

Whereas someone on a recent Python would simply run

    $ pip install -r requirements.txt
    

Since py26-requirements.txt explicitly lists Python 2.6 dependencies only and then relies on requirements.txt, most likely you will only need to update the main requirements when/if new dependencies are needed.

You can check out the [commit][5] where Python 2.6 support for OrderDict has been introduced.

If you want to get in touch, I&#8217;m [@nicolaiarocci][6] on Twitter.

 [1]: https://docs.python.org/2/library/collections.html#collections.OrderedDict
 [2]: http://python-eve.org
 [3]: https://pypi.python.org/pypi/ordereddict
 [4]: http://code.activestate.com/recipes/576693
 [5]: https://github.com/nicolaiarocci/eve/commit/ae292f42a6ea92a447b194aaf17d8447b859b0ab
 [6]: https://twitter.com/nicolaiarocci
