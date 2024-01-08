---
title: Fattura Elettronica Open Source
author: Nicola Iarocci
date: 2015-02-10
url: /fattura-elettronica-open-source/
dsq_thread_id:
  - 3502382189
categories:
  - Programming
tags:
  - .net
  - fattura elettronica
  - open source
---
_this post is about an all-italian open source release, so it&#8217;s going to be in italian_

[FatturaElettronicaPA][1] è un nuovo progetto open source che ho rilasciato qualche giorno fa assieme alla [mia azienda][2]. Si tratta di una libreria C# che permette di leggere, scrivere e convalidare le Fatture Elettroniche aderenti alle specifiche del [sistema di interscambio][3] della Pubblica Amministrazione. <!--more-->

Rilasciata come [Portable Class Library][4], FatturaElettronicaPA gira senza modifiche sui seguenti ambienti:

  * .NET Framework 4.0 e superiori,
  * Xamarin.iOS
  * Xamarin.Android
  * Windows Phone 8
  * Windows Store apps (Windows 8)
  * Silverlight 5.0

## Come usare la Fattura Elettronica PA

Usarla è molto semplice. Prima creiamo una istanza di `FatturaElettronica`:

    // instanzia una nuova fattura elettronica
    FatturaElettronica fattura = new FatturaElettronica();
    

Quindi leggiamo da un file standard SDI. E&#8217; sufficiente passare un `XmlReader` attivo al metodo `FatturaElettronica.ReadXml()`:

    // lettura da file XML compatibile con formato SDI1.1
    var s = new XmlReaderSettings {IgnoreWhitespace = true};
    var r = XmlReader.Create("IT01234567890_11111.xml", s);
    fattura.ReadXml(r);
    

La fattura si aggiorna cambiando i valori delle sue proprietà. Qui aggiorniamo il regime fiscale del mittente. Basterebbe una sola riga di codice; usiamo tre linee per una migliore leggibilità:

    // modifica valore
    var header = fattura.FatturaElettronicaHeader
    var prestatore = header.CedentePrestatore
    prestatore.DatiAnagrafici.RegimeFiscale = "RF11";
    

Convalidare una fattura è un gioco da ragazzi. La proprietà `Error` conterrà tutti gli errori eventualmente riscontrati.

    // convalida documento
    if (!fattura.IsValid) {
        Debug.WriteLine(fattura.Error);
    }
    

Stampiano la fattura come flusso JSON:

    // serializzazione JSON
    var json = fattura.ToJson(JsonOptions.Indented);
    Debug.WriteLine(json);
    

Infine, salvarla su file standard SDI è solo questione di aprire un file con `XmlWriter` e passarlo al metodo `WriteXml`:

    // serializzazione XML secondo lo standard SDI 1.1
    var s = new XmlWriterSettings { Indent = true };
    
    XmlWriter w;
    var fileName = "IT01234567890_11111.xml"
    using (w = XmlWriter.Create(fileName, s)) {
        fattura.WriteXml(w);
    }
    

## Installazione

FatturaElettronicaPA è un package [NuGet][5]. Per installarlo è sufficiente usare la Package Console manualmente:

    PM> Install-Package FatturaElettronicaPA
    

oppure usare la interfaccia di Visual Studio.

## Progetti satellite

`FatturaElettronica` deriva a sua volta da [BusinessObjects][6], una classe che implementa la (de)serializzazione e la convalida base.

[FatturaElettronica.Forms][7] è invece una libreria WinForms che provvede una UI per l&#8217;editing e la segnalazione degli errori di convalida. Al momento supporta l&#8217;intestazione (header) e viene già usato in produzione nel nostro software gestionale:

<div id="attachment_7500" style="width: 1450px" class="wp-caption aligncenter">
  <a href="images/feforms.png" rel="lightbox[7465]"><img src="http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/feforms.png?fit=525%2C328" alt="Fattura Elettronica Open Source" class="size-full wp-image-7500" srcset="http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/feforms.png?w=1440 1440w, http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/feforms.png?resize=150%2C94 150w, http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/feforms.png?resize=300%2C188 300w, http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/feforms.png?resize=1024%2C640 1024w" sizes="(max-width: 525px) 100vw, 525px" data-recalc-dims="1" /></a>
  
  <p class="wp-caption-text">
    FatturaElettronica.Forms in Amica 10 (click per ingrandire.)
  </p>
</div>

In futuro sarebbe utile aggiungere supporto per la visualizzazione e convalida del corpo fattura (Body).

[FatturaElettronica.WebServices][8] consente di interrogare i diversi Web Service della Pubblica Amministrazione dedicati alla fatturazione elettronica. Tutti i progetti relativi alla fatturazione elettronica sono disponibili su [GitHub][1].

## Perché la Fattura Elettronica Open Source?

Dallo scorso 6 Giugno 2014 i Ministeri, le Agenzie fiscali, le scuole e gli enti nazionali di previdenza non accettano più fatture emesse o trasmesse in forma cartacea. A partire dal 31 marzo 2015 la stessa disposizione è estesa agli altri Enti a carattere Nazionale ed a tutte le amministrazioni locali.

L&#8217;adozione delle fatture elettroniche è in pieno svolgimento e non crediamo di sbagliarci immaginando un futuro non troppo remoto in cui questo formato verrà adottato (per imposizione, come ci pare probabile, o per comodità) anche dal settore privato, diventando di fatto lo standard di riferimento.

Noi ci siamo trovati a dover implementare il supporto per la fatturazione elettronica per gli utenti di [Amica 10][2], il nostro software gestionale. Abbiamo pensato che questa fosse una buona occasione per rendere libero il nostro lavoro così che chiunque possa utilizzarlo per mettersi rapidamente al passo e magari decidere di dare una mano in uno dei tanti modi possibili: [segnalando problemi][9], [contribuendo direttamente][1] al progetto, o semplicemente parlandone in giro.

Il software è migliore quando è condiviso.

If you want to get in touch, I am @[nicolaiarocci][10] on Twitter.

 [1]: https://github.com/FatturaElettronicaPA
 [2]: http://gestionaleamica.com
 [3]: http://www.fatturapa.gov.it/export/fatturazione/sdi/Specifiche_tecniche_del_formato_FatturaPA_V1.1.pdf
 [4]: https://msdn.microsoft.com/en-us/library/gg597391%28v=vs.110%29.aspx
 [5]: https://www.nuget.org/packages/FatturaElettronicaPA/
 [6]: https://github.com/FatturaElettronicaPA/BusinessObjects
 [7]: https://github.com/FatturaElettronicaPA/FatturaElettronicaPA.Forms
 [8]: https://github.com/FatturaElettronicaPA/FatturaElettronicaPA.WebServices
 [9]: https://github.com/FatturaElettronicaPA/FatturaElettronicaPA/issues
 [10]: http://twitter.com/nicolaiarocci
