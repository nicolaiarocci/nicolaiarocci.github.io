+++
date = "2018-10-27T09:05:25+02:00"
share = false
title = "FatturaElettronica for .NET v0.9 has been released"
+++

FatturaElettronica for .NET v0.9 has been released. The companion Extensions
package also hits v0.4.

The main new feature is the `FromJson()` extension method which allows, you
guessed it, for deserialization of a JSON stream into a `Fattura` class
instance:

```c#

    var fattura = Fattura.CreateInstance(Instance.Privati);
    fattura.FromJson(new JsonTextReader(new StringReader(json)));
    // or, if FatturaElettronica.Extensions v0.4 is being used:
    fattura.FromJson(json);

    // Invoice is now ready for inspection.
    foreach (var documento in fattura.Body)
    {
        var dati = documento.DatiGenerali.DatiGeneraliDocumento;
        Console.WriteLine($"fatt. num. {dati.Numero} del {dati.Data}");
    }
```

I should probably mention that FatturaElettronica.Core 0.4 is also out, and
that that is the actual place where all the new juice comes from, courtesy of
[Emanuele Zavallone][ez]. You don't have to directly install Core, it will be
pulled down for you by the main packages.

So enjoy, and go get them while they are hot:

- FatturaElettronica for .NET ([nuget][fen], [github][fe])
- FatturaElettronica Extensions ([nuget][fexn], [github][fex])

*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

 [tw]: http://twitter.com/nicolaiarocci
 [nl]: http://eepurl.com/b-_Pzz
 [fe]: https://github.com/FatturaElettronica/FatturaElettronica.NET
 [fen]: https://www.nuget.org/packages/FatturaElettronica/
 [fex]: https://github.com/FatturaElettronica/FatturaElettronica.Extensions
 [fexn]: https://www.nuget.org/packages/FatturaElettronica.Extensions/
 [nuget]: https://www.nuget.org/packages/FatturaElettronica
 [ez]: https://github.com/emazv72