---
title: Cerberus 0.9 has been released
author: Nicola Iarocci
date: 2015-06-30
url: /cerberus-0-9-has-been-released/
categories:
  - Programming
tags:
  - cerberus
  - eve
  - open source
  - python
---
A few days ago [Cerberus 0.9][1] was released. It includes a bunch of new cool features, let&#8217;s browse through some of them.

## Collection rules

First up is the new set of `anyof`, `allof`, `noneof` and `oneof` validation rules. `anyof` allows you to list multiple sets of rules to validate against. The field will be considered valid if it validates against one set in the list. For example, to verify that a property is a number between 0 and 10 or 100 and 110, you could do the following:

    >>> schema = {
    ...     'prop1': {
    ...         'type': 'number',
    ...         'anyof': [
    ...             {'min': 0, 'max': 10}, 
    ...             {'min': 100, 'max': 110}
    ...         
    ...         ]
    ...     }
    ... }
    
    >>> doc = {'prop1': 5}
    >>> v.validate(document, schema)
    True
    
    >>> doc = {'prop1': 105}
    >>> v.validate(document, schema)
    True
    
    >>> doc = {'prop1': 55}
    >>> v.validate(document, schema)
    False

`allof` is the same as `anyof`, except that all rule collections in the list must validate. Same pattern applies to `noneof` (no rule in collection must validate) and `oneof` (only one rule in collection must validate).

## Type coercion

Type coercion allows you to apply a callable to a value before any other validators run. The return value of the callable replaces the new value in the document. This can be used to convert values or sanitize data before it is validated.

    >>> v = Validator({'amount': {'type': 'integer'}})
    >>> v.validate({'amount': '1'})
    False
    
    >>> v = Validator({
    ...     'amount': {
    ...         'type': 'integer', 
    ...         'coerce': int
    ...     }
    ... })
    >>> v.validate({'amount': '1'})
    True
    >>> v.document
    {'amount': 1}
    
    >>> to_bool = lambda v: v.lower() in ['true', '1']
    >>> v = Validator({
    ...     'flag': {
    ...         'type': 'boolean', 
    ...         'coerce': to_bool
    ...     }
    ... })
    >>> v.validate({'flag': 'true'})
    True
    
    >>> v.document
    {'flag': True}
    

## Properties (keys) validation

`propertyschema` is the counterpart to `valueschema` (also new, it replaces the now deprecated `keyschema`) and validates the keys of a dictionary.

    >>> schema = 'a_dict': {
    ...     'type': 'dict', 
    ...     'propertyschema': {
    ...         'type': 'string', 
    ...         'regex': '[a-z]+'
    ...     }
    ... }
    
    >>> document = {'a_dict': {'key': 'value'}}
    >>> v.validate(document, schema)
    True
    
    >>> document = {'a_dict': {'KEY': 'value'}}
    >>> v.validate(document, schema)
    False
    

## List of types

The `type` rule can now be a list of types, to allow for different type of values for the field.

    >>> v = Validator({
    ...     'quotes': {
    ...         'type': ['string', 'list']
    ...     }
    ... })
    
    >>> v.validate({'quotes': 'Hello world!'})
    True
    
    >>> v.validate({'quotes': ['Do not disturb my circles!', 
    ...                        'Heureka!']})
    True
    
    >>> v = Validator({
    ...     'quotes': {
    ...         'type': ['string', 'list'], 
    ...         'schema': {'type': 'string'}
    ...     }
    ... })
    
    >>> v.validate({'quotes': 'Hello world!'})
    True 
    
    >>> v.validate({'quotes': [1, 'Heureka!']})
    False
    
    >>> v.errors
    {'quotes': {0: 'must be of string type'}}
    

And there is more so make sure you check the [changelog][2] before upgrading. No breaking changes but there&#8217;s at least one deprecation, as mentioned.

Fun fact: Cerberus is currently getting 3x the downloads of his sister project [Eve][3], the REST API Framework for which the tool was originally conceived. Interesting if you consider that Eve is featuring 10x the GitHub stars. Fun, but not really surprising since Cerberus probably has a broader audience.

Special thanks to Frank Sachsenheim, Tobias Betz, Brett and C.D. Clark III for their valuable contributions to this release.

If you want to get in touch, I am @[nicolaiarocci][4] on Twitter.

 [1]: https://github.com/nicolaiarocci/cerberus
 [2]: https://cerberus.readthedocs.org/en/latest/#changelog
 [3]: https://github.com/nicolaiarocci/eve
 [4]: http://twitter.com/nicolaiarocci
