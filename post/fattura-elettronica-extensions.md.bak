+++
date = "2018-09-27T11:23:25+02:00"
share = false
title = "Lettura di fatture elettroniche con firma digitale in .NET (.p7m)"
+++
> Sorry folks. Because of its target audience, this post is in Italian.

Ho appena rilasciato [FatturaElettronica.Extensions][fex]. Si tratta di un package che
estende [FatturaElettronica.NET][fe] aggiungendo (per ora) un solo extension method:
`ReadXmlSigned`

Il metodo si affianca all'esistente `ReadXml` ed accetta un file in formato
standard fattura elettronica già firmato digitalmente (estensione .p7m), lo
legge, verifica che le firme siano valide, quindi lo carica in un oggetto
`FatturaElettronica` che lo rappresenta interamente:

```c#

    using System;
    using FatturaElettronica;
    using FatturaElettronica.Extensions;
    using FatturaElettronica.Impostazioni;


    namespace DemoApp
    {
        class Program
        {
            static void Main(string[] args)
            {
                var fattura = Fattura.CreateInstance(Instance.Privati);

                // lettura da file con firma digitale
                fattura.ReadXmlSigned("IT02182030391_31.xml.p7m");

                // la fattura è ora pronta per l'uso
                foreach (var documento in fattura.Body)
                {
                    var dati = documento.DatiGenerali.DatiGeneraliDocumento;
                    Console.WriteLine($"fatt. num. {dati.Numero} del {dati.Data}");
                }
            }
        }
    }
```

Come già per il fratello maggiore, Extensions è rilasciato con [licenza open
source BSD][bsd]. Il package è già [disponibile su nuget][nuget] ed
è NetStandard 2.0, quindi compatibile con un gran numero di piattaforme.

Per informazioni dettagliate vi rimando al repository su [GitHub][fex].

*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

 [tw]: http://twitter.com/nicolaiarocci
 [nl]: http://eepurl.com/b-_Pzz
 [fe]: https://github.com/FatturaElettronica/FatturaElettronica.NET
 [fex]: https://github.com/FatturaElettronica/FatturaElettronica.Extensions
 [bsd]: http://github.com/FatturaElettronica/FatturaElettronica.Extensions/blob/master/LICENSE
 [nuget]: https://www.nuget.org/packages/FatturaElettronica.Extensions/
