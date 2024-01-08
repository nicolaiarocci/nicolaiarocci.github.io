---
title: New Releases for Cerberus and Eve
author: Nicola Iarocci
date: 2015-03-17
url: /new-releases-for-cerberus-and-eve/
categories:
  - Programming
tags:
  - cerberus
  - eve
  - python
---
Yesterday [Cerberus 0.8.1][1] was released with a few little [fixes][2], one of them being more a new feature than a fix really: sub-document fields can now be set as field dependencies by using a &#8216;dotted&#8217; notation.

So, suppose we set the following validation schema:

    schema = {
      'test_field': {
        'dependencies': [
          'a_dict.foo', 
          'a_dict.bar'
        ]
      },
      'a_dict': {
        'type': 'dict',
          'schema': {
            'foo': {'type': 'string'},
            'bar': {'type': 'string'}
          }
      }
    }
    

Then, we can validate a document like this:

    >>> v = Validator(schema)
    >>> document = {
          'test_field': 'foobar', 
          'a_dict': {'foo': 'foo'}
        }
    
    >>> v.validate(document, schema)
    False
    
    >>> v.errors
    {'test_field': "field 'a_dict.bar' is required"}
    

This release will not work with Eve 0.5.2 or less so if you want to use Cerberus 0.8.1 with Eve make sure you upgrade to [Eve 0.5.3][3], released today. By the way, yesterday we hit 2K stargazers and 70 contributors on the [Eve repository][4], quite the milestone!

If you want to get in touch, I am @[nicolaiarocci][5] on Twitter.

 [1]: https://github.com/nicolaiarocci/cerberus
 [2]: https://github.com/nicolaiarocci/cerberus/blob/master/CHANGES
 [3]: https://pypi.python.org/pypi/Eve
 [4]: https://github.com/nicolaiarocci/eve
 [5]: http://twitter.com/nicolaiarocci
