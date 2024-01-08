---
date: 2020-06-06T07:05:25+02:00
title: "FatturaElettronica for .NET v3.0 released"
description: It features full support for latest specifications by the Italian Public Administration (v1.6), and is now delivered with a single package model.
share: false
---

[FatturaElettronica for .NET][fe] 3.0 is now available on [NuGet][ng]. It brings full support for the [latest technical specifications][ts] (v1.6.1) issued by the Italian Public Administration. These come with a number of relevant changes, which were originally supposed to be effective starting May 4, 2020. We were ready well in advance (v3.beta-1 package was available on March 20) but then, because of the COVID19 situation (and, I suspect, pressure from relevant "not-ready-to-deliver" software companies) the deadline was pushed forward to October 1, 2020. 

So yes, you have plenty of time, but the good news is you can upgrade today and spare yourself some of the inevitable pain that comes with uprading your software too close to the deadline. Just download FatturaElettronica 3.0 and upgrade your projects. The new format is mostly backwards-compatible, which means that it will read and write old format (pre-v1.6) XML files just fine. In fact, companies have been using v3.0 beta since March with no issues. I am confident that the upgrade process will be relatively straightforward. 

Just keep in mind that v3 unifies all FatturaElettronica packages (Core, Extensions, and FatturaElettronica itself) into one, single package. This makes all the powerful extension methods available right away, and also simplifies the development, building, and installation processes. If you were using the Extensions package before, and after the upgrade you get warning messages, then you need to uninstall the Extensions and Core packages, which are not needed as stand-alones anymore.

### How to install

.NET CLI:

	dotnet add package FatturaElettronica --version 3.0.0

Package Manager:

	Install-Package FatturaElettronica -Version 3.0.0

Package Reference:

	<PackageReference Include="FatturaElettronica" Version="3.0.0" />

packet CLI:

	paket add FatturaElettronica --version 3.0.0


As always, make sure you read the [changelog][cl]. Most importantly in this case, for a rundown on the new specifications and the upgraded file format, check out the [new specifications][ts]. 

Lastly, this is your friendly reminder that if you are using this package in a revenue-generating project, it is your best interest to consider [supporting it][sp]. 

Enjoy!

*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

[fe]: https://github.com/FatturaElettronica/FatturaElettronica.NET
[ng]: https://www.nuget.org/packages/FatturaElettronica/3.0.0
[sp]: https://fatturaelettronicaopensource.org/#supporta-il-progetto
[ts]: https://www.agenziaentrate.gov.it/portale/documents/20143/2370834/Allegato+A+-+Specifiche+tecniche+vers+1.6_.pdf/a9917ec2-29a3-4f4a-a7d0-93af96fcaad5
[cl]: https://fatturaelettronicaopensource.org/docs/changelog.html
[tw]: http://twitter.com/nicolaiarocci
[nl]: http://eepurl.com/b-_Pzz

