---
title: 'Fattura Elettronica Open Source: Web Service PA'
author: Nicola Iarocci
date: 2015-05-21
url: /fattura-elettronica-open-source-web-service-pa/
categories:
  - Programming
tags:
  - .net
  - fattura elettronica
  - open source
---
_this post is about an all-Italian open source release, so it’s going to be in Italian_

Il progetto [Fattura Elettronica Open Source][1] si è arricchito di un nuovo strumento: [Web Services][2]. Il namespace `FatturaElettronicaPA.WebServices` raccoglie una serie di client C# che consentono di consultare i Web Service per la Fattura Elettronica messi a disposizione dalla Pubblica Amministrazione.

Sono disegnati in maniera da esporre tutti la stessa interfaccia ed essere al tempo stesso semplici e leggeri. Al momento lavorano in modalità sincrona ma l&#8217;obiettivo è di renderli tutti asincroni.

## Come usare i Web Service

Prendiamo per esempio il Web Service che consente di convalidare un Codice Univoco di Fatturazione e recuperare le informazioni relative all&#8217;ufficio:

    var ws = new CodiceUnivocoFatturazioneWebService()
    
    // Authorization Id ricevuto dall'ente.
    ws.AuthId = "<auth Id>";
    // Codice univoco dell'ufficio che ci interessa
    ws.CodiceUfficio = "KN3VNW";
    
    ws.PerformRequest();
    if (ws.Ufficio == null) return;
    
    // "Ravenna"
    Console.WriteLine(ws.Ufficio.Comune);
    

Molto semplice. Gli altri WebService (sono sette in tutto) operano secondo lo stesso schema. Ricordo che per l&#8217;utilizzo dei Web Services della Pubblica Amministrazione è necessario richiedere una specifica autorizzazione. L&#8217;Authorization Id è gratuito ed il rilascio è immediato, ma bisogna compilare un apposito [questionario][3].

## Installazione

FatturaElettronicaPA.WebServices è su [NuGet][4] quindi tutto quel che serve è eseguire:

    PM> Install-Package FatturaElettronicaPA.WebServices
    

dalla Package Console, oppure usare il comando equivalente in Visual Studio.

La libreria è una portable class library e gira senza modifiche sui seguenti ambienti: .NET Framework 4.0 e superiori; Xamarin.iOS; Xamarin.Android; Windows Phone 8; Windows Store apps (Windows 8); Silverlight 5.0. Enjoy!

If you want to get in touch, I am @[nicolaiarocci][5] on Twitter.

 [1]: http://nicolaiarocci.com/fattura-elettronica-open-source/
 [2]: https://github.com/FatturaElettronicaPA/FatturaElettronicaPA.WebServices
 [3]: http://www.indicepa.gov.it/registr-user-ws/ws-registrazione-start.php
 [4]: https://www.nuget.org/packages/FatturaElettronicaPA.WebServices/
 [5]: http://twitter.com/nicolaiarocci
