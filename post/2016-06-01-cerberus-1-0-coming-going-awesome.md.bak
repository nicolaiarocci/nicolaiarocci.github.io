---
title: Cerberus 1.0 is coming and it is going to be awesome
author: Nicola Iarocci
date: 2016-06-01
url: /cerberus-1-0-coming-going-awesome/
categories:
  - Programming
tags:
  - cerberus
  - open source
  - python
---
[Cerberus][1] is a lightweight and extensible data validation library for Python. Beta has been around since 2012. During this time Cerberus has been serving as the validation system for [Eve][2] core. It has been also adopted by a [quite a lot][3] open source projects, averaging around 18K downloads per month on PyPI and collecting some remarkable [endorsements][4].

All things considered, I would dare to claim that Cerberus is battle tested to death. This is, in fact, one reason why I believe that the time for a canonical and stable release has come. Another reason is that next release is a major one. It brings a ton of important [new features][5] along with very significant code refactoring and a redesigned, powerful [API][6]. Third, next release [breaks][7] backward compatibility, and we want to signal that in the version number.

So next Cerberus release will be 1.0. If you have been following the development this will come as no surprise, as a Release Candidate has been out for a while. As a Cerberus user you will want to take the plunge and upgrade to 1.0 because well, it is just too cool to be true. If new to Cerberus you will also want to adopt 1.0 right away, for the same reason. If you are new however, make sure you get the [basics covered][8] before reading further. By the way, at latest PyCon Italy I gave a talk on Cerberus which also included a preview of several 1.0 features. You can check the [slides][9] to get a general idea of the tool, its usage, and upcoming features.

Let&#8217;s now look at some of the relevant features and changes introduced with Cerberus 1.0. For a (mostly) accurate list of changes and new features, have a look at the [changelog][5].

<!--more-->

## Transformation and normalization

Big news in the normalization department. Similar to `validated()`, the new `normalized()` method returns a normalized copy of a document without validating it.

{{< gist nicolaiarocci d67e66bd0970225cfdd032952d9ed651 >}}

### Renaming of Fields

You can now define a field to be renamed before any further processing.

{{< gist nicolaiarocci 19346b40a34a3a99f512d3a9e97744b2 >}}

To let a callable rename a field or arbitrary fields, you can define a handler for renaming. If the constraint is a string, it points to a custom method.

{{< gist nicolaiarocci 2eddf9ae965e66f7b2ed7bb84453dd2e >}}

If the constraint is an iterable, the value is processed through that chain.

{{< gist nicolaiarocci 0b9f72c1e6f480f90cb845adc26b28f5 >}}

### Purging Unknown Fields

After renaming, unknown fields will be purged if the `purge_unknown` property of a `Validator` instance is `True`.

{{< gist nicolaiarocci 2bc43cfb27b4148a50a217ee6fae9671 >}}

You can set the property per keyword-argument upon initialization or as rule for subdocuments like `allow_unknown`. The default is `False`.

### Default Values

You can set default values for missing fields in the document by using the default rule.

{{< gist nicolaiarocci 829129d3a30dcf29aadee2173139690d >}}

You can also define a default setter callable to set the default value dynamically. The callable gets called with the current (sub)document as the only argument. If the constraint is a string, it points to a custom method.

{{< gist nicolaiarocci a9731d22994c23312f9c2569d3c58e02 >}}

### Value Coercion

Coercion has been introduced with 0.9. It allows you to apply a callable to a value before the document is validated. The return value of the callable replaces the new value in the document. This can be used to convert values or sanitize data before it is validated.

{{< gist nicolaiarocci 85ba0667defc1f54486ce45b851ca548 >}}

If the constraint is an iterable, the value is processed through that chain.

{{< gist nicolaiarocci 20fd9437713f77d4cc9365162b5675eb >}}

Please note that `coerce` kicks in with `validate()`, not with `normalized()`.

## Schema Validation

This is another area the is seeing a lot of changes and new, powerful things.

### Registries

Schema registries are awesome if your schemas shall include references to themselves (recursion) and if they contain a lot of reused parts and are supposed to be serialized. There are two default registries in the cerberus module namespace. You can use `schema_registry` to store definitions for schemas which can later be re-used:

{{< gist nicolaiarocci d7bf19da6a6505bacf7a4be7ad0058d1 >}}

And you can extend `rules_set_registry` with rules-sets which can then be referenced in validation schemas:

{{< gist nicolaiarocci c82f6a8e255cd408d02afca8d2be0012 >}}

### Schema Constraints in docstrings

Validation schemas themselves are validated when passed to the validator or a new set of rules is set for a document’s field. A `SchemaError` is raised when an invalid validation schema is encountered.

Now you can provide constraints as literal Python expression in the docstring of the rule’s implementing method to validate the arguments given in a schema for that rule. Either the docstring contains solely the literal or the literal is placed at the bottom of the docstring preceded by the following sentence: `The rule's arguments are validated against this schema`.

The example below is comes directly from Cerberus&#8217; own test suite:

{{< gist nicolaiarocci 71575bca60ba1993e5e59cdc3f3a9f1a >}}

## Validation Rules

### `forbidden`

Opposite to `allowed`, this new rule validates if a value is any but one of the defined values:

{{< gist nicolaiarocci b7ea2a0170c2e67e0b1c5d59cff80879 >}}

### `min`, `max`

Up to 0.9 you could only use `min` and `max` to compare numeric types. Now they define minimum and maximum values allowed for any types that implement comparison operators.

{{< gist nicolaiarocci 2e356654c5bd0f98f95473bf27ef2d2e >}}

### `keyschema`

For better consistency, the `propertyschema` rule has been renamed to `keyschema`. This is the counterpart to `valueschema` and validates the _keys_ of a `dict`.

{{< gist nicolaiarocci f553cf446a986058a836a08206076573 >}}

### `type`

Data type validation now also supports the `binary` type.

## Breaking Changes

This is a major release which breaks backward compatibility in several ways. Don&#8217;t worry, these changes are for the better. However, if you are upgrading, then you should really take the time to read the list of changes in the [changelog][5] and consider their impact on your codebase, especially so if you have custom validators sitting around. For your convenience, there are also some [upgrade notes][10] available.

## Acknowledgements

Cerberus 1.0 would not exist in its current form without the incredible work done by Frank &#8220;[funkyfuture][11]&#8221; Sachsenheim. After his initial, timid, set of v0.9 contributions, Frank went on a rage. He really adopted the project and went on touching on every aspect of it: documentation, new features, proposal, fixes, refactoring, ticket triaging, you-name-it. His efforts have been instrumental in taking the project to the next level. As a token of appreciation for his work, I&#8217;m tagging this release with the `funkyfuture` codename.

Of course he was not alone. Other contributors were Matthew Ellison, Dominik Kellner, Damián Nohales, calve, Roman Redkovich. And then are all the other people who helped by opening tickets and spreading the word around. Thank you all, folks.

## Closing notes

Cerberus 1.0 is an important milestone. I consider the API to be reasonably stable and, once it is released, I plan to let it settle down for a while. Release Candidate will stay out for a couple more weeks, which is ideal for you to experiment a little bit before the final release.

If you are a Eve user you probably see the potential that new Cerberus can offer to your RESTful API, especially in the normalization department. Don&#8217;t get too excited though as I do not plan on immediately adding Cerberus 1.0 to Eve. Next Eve release (v0.7), which is also upcoming, will be focused on MongoDB Aggregation Framework and other things. That is more than enough for a major release. I am targeting the following release (v0.8) for Cerberus 1.0 support.

So, have fun with New Cerberus. As usual, please report any issue on the [ticket][12] system.

If you want to get in touch, I am [@nicolaiarocci][13] on Twitter.

 [1]: http://python-cerberus.org
 [2]: http://python-eve.org
 [3]: https://github.com/search?q=from+cerberus+import+Validator&type=Code&utf8=%E2%9C%93
 [4]: https://speakerdeck.com/nicola/cerberus?slide=56
 [5]: http://docs.python-cerberus.org/en/latest/changelog.html#version-1-0
 [6]: http://docs.python-cerberus.org/en/latest/api.html
 [7]: http://docs.python-cerberus.org/en/latest/changelog.html#breaking-changes
 [8]: https://cerberus.readthedocs.io/en/latest/usage.html#cerberus-usage
 [9]: https://speakerdeck.com/nicola/cerberus
 [10]: http://docs.python-cerberus.org/en/latest/upgrading.html
 [11]: https://github.com/funkyfuture
 [12]: https://github.com/nicolaiarocci/cerberus/issues
 [13]: https://twitter.com/nicolaiarocci
