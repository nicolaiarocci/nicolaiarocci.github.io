---
date: 2019-03-13T09:05:25+02:00
title: "FatturaElettronica for .NET v2.0"
description: FatturaElettronica for .NET version 2.0 is out today. It brings support for Fattura Semplificata, at the cost of few minor breaking changes.
share: false
---

Today I pushed version 2.0 of [FatturaElettronica][fe] to NuGet. This release
comes with full support for [Fattura Semplificata][fs], something that has
been on the back-burner for a while. Special thanks to [Gaetano Pizzol][gp]
for single-handly contributing this feature.

Now for the bad news. Since we were to add a new invoice type whereas so far
we only had one, I decided to take the plunge and break backward
compatibility a little bit. The relevant changes are as follows:

1. `Fattura` class renamed as `FatturaOrdinaria`;
2. `FatturaOrdinaria`, its whole hierarchy, and validators moved to the new `FatturaElettronica.Ordinaria` namespace;

These changes leave us with what I think is a cleaner and symmetric API surface. We now have:

1. `FatturaOrdinaria.cs` in the `FatturaElettronica.Ordinaria` namespace;
2. A new `FatturaSemplificata.cs` in the `FatturaElettronica.Semplificata` namespace;
3. A new `FatturaBase` abstract class in root `FatturaElettronica` namespace;

So yes, you will have to recompile after the update. However, you will find
that the changes needed are marginal:

    # using FatturaElettronica;
    using FatturaElettronica.Ordinaria;  # new

    # var fattura = new Fattura();
    var fattura = new FatturaOrdinaria();  # new

Satellite projects [Core][fc], [Extensions][fx], and [Forms][fx] are also
available on NuGet with a matching version number. By the way, in case you
did not know, the Extensions package just recently saw the addition of a
`WriteHtml` extension method, prompted by [Alessandro Scardova][as].

I want to take a moment to mention the vibrant community that is growing
around this project. As of today, we count [ten contributors][c] to the main
project alone, and many others have been chiming in either by opening
tickets, mailing me, or providing suggestions at the various events that I
attend. The contribution rate is a meaningful metric to me. After the years
spent in the Python open-source community, I came back hoping I could help
and encourage the growth of the Italian open source movement within the .NET
eco-system.

Considering the relatively small audience for this project, the adoption rate
is also satisfying. I think the main package recently surpassed 13K
downloads.

*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

 [tw]: http://twitter.com/nicolaiarocci
 [nl]: http://eepurl.com/b-_Pzz
 [fs]: https://www.agenziaentrate.gov.it/wps/content/Nsilib/Nsi/Schede/Comunicazioni/Fatture+e+corrispettivi/Fatture+e+corrispettivi+ST/ST+invio+di+fatturazione+elettronica/?page=ivacomimp
 [gp]: https://github.com/tanogae
 [fe]: https://github.com/FatturaElettronica/FatturaElettronica.NET
 [fc]: https://github.com/FatturaElettronica/FatturaElettronica.Core
 [fx]: https://github.com/FatturaElettronica/FatturaElettronica.Core
 [ff]: https://github.com/FatturaElettronica/FatturaElettronica.Forms
 [as]: https://github.com/AlexBream
 [c]: https://github.com/FatturaElettronica/FatturaElettronica.NET/graphs/contributors