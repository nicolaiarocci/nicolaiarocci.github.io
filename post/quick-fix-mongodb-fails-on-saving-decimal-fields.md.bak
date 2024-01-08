+++
date = "2017-11-23T11:05:28+01:00"
share = false
title = "Quick fix: MongoDB fails when saving Decimal fields"
+++
So today I was trying to store some decimal fields on a MongoDB 3.4
instance and I kept failing, miserably.  

In [Compass][1] I was getting a somewhat obscure "connection lost" message on
every save attempt. Upgrading to Mongo 3.4.10 (I was on 3.4.4) improved things,
as the error message was now hinting at the `setFeatureCompatibilityVersion`
setting which, apparently, was preventing some features to be made available.

Now that made sense, as this specific database had been upgraded all
the way from up Mongo 2.6. A [quick lookup][2] revealed that, when upgrading to
3.4, `setFeatureCompatibilityVersion` is automatically set to `"3.2"`. As we
all know, support for Decimal type only comes with Mongo 3.4.

Setting `setFeatureCompatibilityVersion` to `"3.4"` was the obvious fix, and
I am now happily storing decimals with my documents. As I was on a standalone
dev instance all I had to do was hop on the mongo shell and fire the following
command:

    db.adminCommand( { setFeatureCompatibilityVersion: "3.4" } )

If you are on a replica set, then make sure to hit your primary with the above
command. For all the details, see the [documentation][2].

*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

 [tw]: http://twitter.com/nicolaiarocci
 [nl]: http://eepurl.com/b-_Pzz
 [1]: https://www.mongodb.com/products/compass
 [2]: https://docs.mongodb.com/master/reference/command/setFeatureCompatibilityVersion/#dbcmd.setFeatureCompatibilityVersion

