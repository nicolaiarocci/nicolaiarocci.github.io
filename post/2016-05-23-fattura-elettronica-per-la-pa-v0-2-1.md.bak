---
title: Fattura Elettronica per la PA v0.2.1
author: Nicola Iarocci
date: 2016-05-23
url: /fattura-elettronica-per-la-pa-v0-2-1/
categories:
  - Programming
tags:
  - .net
  - open source
---
Ho appena pubblicato su NuGet l&#8217;ultimo aggiornamento di [FatturaElettronicaPA][1], il package .NET per la compilazione e convalida delle fatture elettroniche per la Pubblica Amministrazione. Si tratta della [versione 0.2.1][2] che fa proprie le novità annunciate il 9 Maggio scorso:

> A partire dal 9 maggio 2016 sono introdotti nuovi controlli sui file trasmessi al Sistema di Interscambio. Per consentire il necessario adeguamento al nuovo regime di verifiche, fino al 31 luglio 2016 il mancato superamento di uno o più di questi nuovi controlli non comporterà lo scarto del file ma solo una segnalazione che verrà riportata all’interno della Ricevuta di consegna o della Notifica di mancata consegna. Dal 1 agosto 2016 i file che non dovessero superare uno o più di questi controlli verranno scartati. 

Se per ora i nuovi controlli non sono vincolanti, lo saranno a partire dal 1 agosto. Poiché si tratta di una serie di convalide sui conteggi consiglio di passare alla versione 0.2.1 al più presto, così da verificare che in effetti le vostre fatture elettroniche siano in linea con le aspettative della PA: potreste avere qualche sorpresa.

Nel nostro caso, per esempio, abbiamo dovuto prendere atto che gli importi imponibili relativi alle aliquote IVA, così come le corrispondenti imposte, devono essere indicati al lordo degli eventuali sconti generali del documento, pena il rifiuto dello stesso da parte del sistema di interscambio. Date una occhiata al [changelog][3] per l&#8217;elenco completo delle novità.

Voglio aggiungere un commento sulle modalità di pubblicazione degli aggiornamenti tecnici da parte di Agenzia Entrate/Sogei. Sebbene siano dotati di data e numero di versione, questi sono da considerarsi, ad essere buoni, puramente indicativi. Per esempio l&#8217;attuale [versione 1.2][4] dell&#8217;elenco controlli è stata aggiornata &#8220;silenziosamente&#8221; un paio di giorni dopo la pubblicazione (hanno aggiunto una tolleranza di 1 Euro al controllo 00422). Così lo sviluppatore incauto che si limiti a controllare la data e il numero di versione del documento rischia di vedersi respingere fatture per lui del tutto corrette, a meno che non di prenda la briga di verificare, riga per riga, la corrispondenza tra la documentazione in suo possesso e quella disponibile sul sito in quel momento. Chiaramente in PA non hanno idea di cosa sia il [Semantic Versioning][5].

Un ringraziamento al mio collega Stefano Gardini. Il suo nome non compare nelle commit ma, quando si stratta di fatturazione e contabilità, è come se ci fosse.

If you want to get in touch, I am [@nicolaiarocci][6] on Twitter.

 [1]: https://github.com/FatturaElettronicaPA/FatturaElettronicaPA/
 [2]: https://www.nuget.org/packages/FatturaElettronicaPA/0.2.1
 [3]: https://github.com/FatturaElettronicaPA/FatturaElettronicaPA/blob/master/CHANGES
 [4]: http://www.fatturapa.gov.it/export/fatturazione/sdi/Elenco_Controlli_V1.2.pdf
 [5]: http://semver.org/
 [6]: https://twitter.com/nicolaiarocci
