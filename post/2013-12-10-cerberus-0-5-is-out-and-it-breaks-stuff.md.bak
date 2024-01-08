---
title: Cerberus 0.5 is out (and it breaks stuff)
author: Nicola Iarocci
date: 2013-12-10
url: /cerberus-0-5-is-out-and-it-breaks-stuff/
dsq_thread_id:
  - 2041332891
categories:
  - Programming
tags:
  - cerberus
  - eve
---
The new release changes the way validation errors are reported. Please note that these changes will also affect future releases of [Eve][1], the Python REST API Framework.

What we had before was basically a list of human-readable errors. Each item in the list, while perfectly fine for human reading, wasn't really ideal for algorithmic parsing. Why would you want to parse the errors with an algorithm? A common case would be when your client is using business objects to represent API resources (think a client-side ORM), and would have a hard time binding validation errors to the objects themselves.<!--more-->

So for example, previously we had:

    [
        "min value for field age is 10",
        "value of field name must be of string type"
    ]

With Cerberus 0.5+ we now have:

{
    age: min value is 10,
    name: must be of string type
}

Let's look at more complex structures, like lists. Imagine we have a schema defined like this:

    schema = {
        'list_of_values': {
            'type': 'list',
            'items': [{'type': 'string'}, {'type': 'integer'}]
        }
    }

And this is the document we want to validate against it:

    document = {
        'a_list_of_values': ['a string', 'not an integer']
    }

Validation will of course fail and, given the new dictionary format, inspecting the errors property will return the following:

    >>> v = Validator(document, schema)
    False
    
    >>> v.errors
    {1: 'must be of integer type'}

Let's look at a document that contains a list of dictionaries instead:

    document = {
        rows: [
            {'sku': 1, 'price': 100},
            {'sku': 'hello', 'price': '1'}
        ]
    }

Validation errors will be reported like this:

    {
        rows: {
            0: {
                'sku': 'must be of string type',
                'price': 'must be of integer type'
            },
            1: {
                'price': 'must be of integer type'
            }
        }
    
    }

By contrasts, on top of my memory, any previous Cerberus release would report:

    [
        "rows[0]": 'field "sku" in must be of string type',
        "rows[0]": 'field "price" in must be of integer type',
        "rows[1]": 'field "price" in must be of integer type'
    ]

As you can easily see, the old implementation was forcing the client to properly parse the list in order to retrieve line number, offending field and the actual error. Overall Im fairly confident that this is an important step forward. Checkout the [documentation][2], which has been updated to reflect the changes.

Get [Cerberus 0.5][3] while its hot.

 [1]: http://python-eve.org
 [2]: http://cerberus.readthedocs.org/en/latest/
 [3]: https://crate.io/packages/Cerberus/
