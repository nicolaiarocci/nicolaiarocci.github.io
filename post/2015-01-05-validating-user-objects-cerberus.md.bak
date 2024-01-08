---
title: Validating user objects with Cerberus
author: Nicola Iarocci
date: 2015-01-05
url: /validating-user-objects-cerberus/
dsq_thread_id:
  - 3391491253
categories:
  - Programming
tags:
  - cerberus
  - python
---
People keep telling me that they want to validate class and instance attributes (object properties) with [Cerberus][1]. While it certainly wasn&#8217;t conceived with that goal in mind, it is actually very possible to leverage both the Python [data model][2] and Cerberus [extensibility][3] to achieve object validation.

## Nuts & Bolts

Let&#8217;s say that we have a simple class:

    >>> class Person(object):
    ...     pass
    

We create a `Person` instance and add a few properties and values:

    >>> p = Person()
    >>> p.name = "bill"
    >>> p.age = 44
    

Now let&#8217;s instance a Cerberus Validator and set up some validation rules for it:

    >>> from Cerberus import Validator
    >>> schema = {
    ...     'name': {'type': 'string'},
    ...     'age': {'type': 'integer', 'min': 0}
    ... }
    >>> v = Validator(schema)
    

As you probably know already, all Python user objects have a `__dict__` magic method which exposes class and instance attributes as a dictionary. This means that we can also query our class like this:

    >>> p.__dict__
    {'name': 'bill', 'age': 44}
    
    >>> p.__dict__['age']
    44
    

You see where we are going with this: we can exploit the `__dict__` method in order to let Cerberus perform validation on our object:

    >>> v.validate(p.__dict__)
    True
    

Validation succeeds because current attribute values do not break any rule. However, if we break the rules we do get what we deserve:

    >>> p.age = -1
    >>> v.validate(p.__dict__)
    False
    
    >>> v.errors
    {'age': 'min value is 0'}
    

This works, but is somewhat clumsy. We can do better.

## A Custom Object Validator

How about letting the Validator do the work for us? We could subclass the standard Validator and extend it to natively support object validation.

    >>> class ObjectValidator(Validator):
    ...     def validate_object(self, obj):
    ...         return self.validate(obj.__dict__)
    ...
    
    >>> v = ObjectValidator(schema)
    >>> v.validate_object(p)
    False
    
    >>> v.errors
    {'age': 'min value is 0'}
    
    >>> p.age = 44
    >>> v.validate_object(p)
    True
    

Much better. But what happens if we add a new property and then validate the object?

    >>> p.lastname = 'white'
    >>> v.validate_object(p)
    False
    
    >>> v.errors
    {'lastname': 'unknown field'}
    

Validation fails because by default unknown fields are not allowed. This might not be the desired behaviour. If this is the case, we simply need to update the helper method in our custom validator class:

    >>> class ObjectValidator(Validator):
    ...     def validate_object(self, obj):
    ...         self.allow_unknown = True
    ...         return self.validate(obj.__dict__)
    
    >>> v.validate_object(p)
    True
    

By setting `allow_unknown` to `True` we [let unknown fields be ignored][4] by validation. If we are not concerned by state changes between calls we might conveniently choose to move the setting of `allow_unknown` to the `__init__` method so it gets executed only once.

Looks good so far. We can validate simple objects. But what about complex ones like those exposing other objects as attributes? This is going to require some more tinkering.

## Validating Complex Objects

It would be super handy if we could add support for an `object` data type and then provide a validation schema for it, like we already do with the `dict` and `list` types. A revised validation schema would then look like this:

    >>> schema = {
    ...     'name': {'type': 'string'},
    ...     'age': {'type': 'integer', 'min': 0},
    ...     'address': {
    ...         'type': 'object',
                'schema': {
    ...             'street': {'type': 'string'},
    ...             'zip': {'type': 'integer'}
    ...         }
    ...     }
    ... }
    

We could then validate it like so:

    >>> class Address
    ...     pass
    
    >>> addr = Address()
    >>> addr.street = 'Lexington'
    >>> addr.zip = 50238
    >>> p.address = addr
    
    >>> v.validate_object(p)
    True
    
    >>> p.address.zip = 'not a number'
    >>> v.validate_object(p)
    False
    
    >>> v.errors
    {'address': {'zip': 'must be of integer type'}}
    

It turns out this is also very achievable. We can leverage Cerberus [data type extensibility model][5] to add support for the `object` type. Then it is just a matter of handling the new type when validating the `schema` rule. I&#8217;m not going into details here but you can check [Validating complex objects with Cerberus][6], a trivial implementation I posted as a GitHub gist.

## Closing note

You might be wondering why don&#8217;t I add object validation to Cerberus core. Actually, I don&#8217;t rule out this possibility but see I like to keep tools as simple, targeted and focused as possible. Besides, there are other object validation tools out there, so adding a new flavour does not seem very useful to me (but let me know if you feel otherwise.) Though as we have seen, if you want to validate user objects with Cerberus, you can do that easily enough.

If you want to get in touch, I am @[nicolaiarocci][7] on Twitter.

 [1]: https://github.com/nicolaiarocci/cerberus
 [2]: https://docs.python.org/2/reference/datamodel.html
 [3]: http://cerberus.readthedocs.org/en/latest/#custom-validators
 [4]: http://cerberus.readthedocs.org/en/latest/#allowing-the-unknown
 [5]: http://cerberus.readthedocs.org/en/latest/#adding-new-data-types
 [6]: https://gist.github.com/nicolaiarocci/829c98eb5f8b4e9c96c1
 [7]: http://twitter.com/nicolaiarocci
