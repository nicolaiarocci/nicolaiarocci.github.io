+++
date = "2017-10-05T09:37:00+02:00"
share = false
title = "Spesometro Open Source per .NET"
+++
*apologies, this post is about an Italian open source release, so it’s
going to be in Italian*

[Spesometro.NET][1] è un nuovo progetto open source che ho rilasciato con la [mia
azienda][2]. Si tratta di un package .NET che permette di leggere, scrivere
e convalidare lo Spesometro o, come è chiamato formalmente, la Comunicazione
delle Fatture Emesse e Ricevute. 

Si tratta di un adempimento che in tempi recenti, per ragioni che non è il caso
di affrontare in questo articolo, ha causato grosse difficoltà sia ai fornitori
di soluzioni software che, e soprattutto, agli utenti finali di dette
soluzioni.

Vista la nostra attività, anche noi ci siamo trovati subito in prima linea,
schiacciati tra l'incudine (l'aspettativa di migliaia di piccole aziende che
usano il software [Amica][2]) e il martello (le scadenze incalzanti
e i problemi tecnici imposti dalla Pubblica Amministrazione). Non senza
difficoltà siamo riusciti a consegnare la soluzione una settimana prima della
scadenza ufficiale (alla quale sono seguite diverse proroghe, ma questa
è un'altra storia).

Come già fatto in passato per la [Fattura Elettronica][7], anche per questo
progetto abbiamo deciso il rilascio con licenza open source. Potete
contribuire al codice, aprire ticket laddove necessario, installarlo ed usarlo
nelle vostre applicazioni. In questo articolo vediamo come usarlo.

### Caratteristiche di Spesometro.NET
Il package mette a disposizione una classe `Spesometro` che rappresenta per
intero il [tracciato ufficiale][3] dello Spesometro 2017. Una istanza di questa
classe può essere usata per leggere, modificare e salvare un file spesometro
conforme allo standard. E' anche disponibile una intera collezione di
validatori che consentono di certificare che lo Spesometro sia conforme alle
regole di convalida ufficiali.

Spesometro.NET è rilasciato una licenza libera [BSD][6] ed è [NetStandard
2.0][4], cosa che consente di utilizzarlo su un ampio numero di piattaforme.

### Come usare Spesometro.NET
Sul repository su GitHub troverete una semplice applicazione NetCore di
esempio. La stessa è anche disponibile nel [README][5] a corredo. esempio. Qui
ne ripercorriamo le caratteristiche principali.

Leggere uno spesometro già esistente è semplice quanto leggere un qualunque
file XML:

{{< gist nicolaiarocci 7cc61d67968014251018309fd76bb233 >}}

Una volta caricato uno spesometro possiamo manipolarlo liberamente.
Qui aggiungiamo alle fatture emesse un committente (cliente) con una nostra
fattura emessa nei suoi confronti.

{{< gist nicolaiarocci caa1db341314bb10a85c47e01397e9ae >}}

I validatori consentono di assicurarsi che le proprietà siano impostate
correttamente rispetto alle regola di convalida previste dallo standard.

{{< gist nicolaiarocci e9c08dc66e1df5f5a2f3eb991edcf07a >}}

Infine, salvare lo spesometro su file un XML conforme alle
specifiche della PA è banale:

{{< gist nicolaiarocci 4a5efe298d9ea3df47513acbff41af82 >}}

Ricordo che il file così creato dovrà essere firmato digitalmente prima di
poter essere consegnato, pena il rigetto. Per quanto riguarda il nome del file,
va rispettata una convenzione. Il file avrà sempre un nome costruito questo
modo: `IT<codicefiscaleazienda>_DF_<progressivounivoco>.XML`. Il codice univoco
di presentazione può essere numerico o alfanumerico, e deve sempre essere di
cinque caratteri. Un esempio potrebbe essere: `IT01180680937_DF_00001.XML`. Le
lettere devono essere sempre maiuscole, altrimenti il file verrà scartato. 

### Installazione
Spesometro è un package NuGet quindi tutto quel che serve è eseguire
`Install-Package Spesometro` dalla Package Console o dalla command line, oppure
usare il comando equivalente in Visual Studio.

### Conclusioni
Rilasciare il progetto [Fattura Elettronica][7] con licenza open source si
è rivelata una ottima iniziativa e, viste le difficoltà in cui molti si trovano
con lo Spesometro, crediamo e speriamo di fare cosa buona e giusta anche con
questo secondo rilascio. Come al solito non esistate a mettervi in contatto per
qualunque suggerimento, consiglio, o problema riscontrato.

PS: nota a margine, anche Fattura Elettronica è stato aggiornato. La versione
0.7 è su nuget, ed è anch'essa NetStandard compatibile.

*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

[1]: https://github.com/FatturaElettronica/Spesometro.NET
[2]: http://gestionaleamica.com
[3]: http://www.agenziaentrate.gov.it/wps/file/Nsilib/Nsi/Strumenti/Specifiche+tecniche/Specifiche+tecniche+comunicazioni/Fatture+e+corrispettivi+ST/Allegato+XML+Dati+Fattura/Formato+XMLdati_fattura.xls
[4]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.0.md
[5]: https://github.com/FatturaElettronica/Spesometro.NET/blob/master/README.md
[6]: https://raw.githubusercontent.com/FatturaElettronica/Spesometro.NET/master/LICENSE
[7]: https://github.com/FatturaElettronica/FatturaElettronica.NET
[tw]: http://twitter.com/nicolaiarocci
[nl]: http://eepurl.com/b-_Pzz
