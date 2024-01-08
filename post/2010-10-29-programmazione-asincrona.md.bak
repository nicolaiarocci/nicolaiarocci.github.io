---
title: 'Programmazione Asincrona per C# e VB'
author: Nicola Iarocci
date: 2010-10-29
url: /programmazione-asincrona/
robotsmeta:
  - index,follow
short-url:
  - http://bit.ly/frlGYm
socialize_text:
  - 'Condividi la tua opinione con gli altri lettori oppure chiedi chiarimenti <a href="#comments">lasciando un commento</a>. Puoi anche <a href="http://nicolaiarocci.com/feed/" title="Syndicate this site using RSS">iscriverti al feed <abbr title="Really Simple Syndication">RSS</abbr></a> per tenerti aggiornato/a sugli articoli pubblicati. Ciao e grazie, Nicola.'
socialize:
  - 1,2
dsq_thread_id:
  - 2081201435
categories:
  - Programming
tags:
  - .net
  - c
  - vb-net
---
Un articolo sul <a title="Making Asynchronous Programming Easy" href="http://blogs.msdn.com/b/somasegar/archive/2010/10/28/making-asynchronous-programming-easy.aspx#" target="_blank">Somasegar&#8217;s Weblog</a> annuncia oggi il rilascio imminente di un nuovo modello di programmazione asincrona per C# and VB:

> Today, we are unveiling significant language and framework enhancements in C# and Visual Basic that enable developers to harness asynchrony, letting them retain the control flow from their synchronous code while developing responsive user interfaces and scalable web applications with greater ease.   This CTP delivers a lightweight asynchronous development experience as close to the standard synchronous paradigms as possible, while providing an easy on-ramp to the world of concurrency

Lo stesso Somasegar riconosce che finora sviluppare applicazioni asincrone complesse con la piattaforma .NET non è stato facile. Tempo fa l&#8217;ho sperimentato in prima persona. Lavoravo su [Amica Prodigy Backup][1], una applicazione di backup remoto.

<div id="attachment_2054" style="width: 490px" class="wp-caption aligncenter">
  <a href="http://gestionaleamica.com/Backup/"><img class="size-full wp-image-2054" title="Amica Prodigy Backup" src="http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/backup1.png?w=480" alt="Amica Prodigy Backup" srcset="http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/backup1.png?w=509 509w, http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/backup1.png?resize=150%2C74 150w, http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/backup1.png?resize=300%2C149 300w, http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/backup1.png?resize=500%2C249 500w" sizes="(max-width: 509px) 100vw, 509px" data-recalc-dims="1" /></a>
  
  <p class="wp-caption-text">
    Applicazione di Backup Remoto Asincrona sviluppata in .NET
  </p>
</div>

Il programma invia files di grandi dimensioni al servizio di cloud storage [S3][2] aggiornando l&#8217;interfaccia utente con lo stato del trasferimento e consentendo nel frattempo di operare liberamente con l&#8217;interfaccia. Devo ammettere che si è trattata di una sfida molto accattivante. Lavoravo per la prima volta su sistemi cloud e c&#8217;era molto da imparare. La parte più difficile fu naturalmente la gestione dei processi asincroni sul client, che era una applicazione WinForm scritta su .NET Framework.

Una rapida occhiata al codice di esempio presente nell&#8217;articolo di Somasegar è meglio di mille parole. &#8216;The Old Way&#8217; vs &#8216;The New Way&#8217; ha un vincitore evidente, ed è la New Way. Mi piace molto il concetto della nuova keyword Await, è una soluzione così elegante! Come sempre in questi casi occorrerà scendere nei dettagli per verificare l&#8217;affidabilità di questa nuova soluzione.

La  CTP è già disponibile per il <a title="Download the new Asynchronous Programming CTP" href="http://www.microsoft.com/downloads/en/details.aspx?FamilyID=18712f38-fcd2-4e9f-9028-8373dc5732b2&displaylang=en" target="_blank">download</a>, attualmente solo per le versioni inglesi di Visual Studio 2010.

 [1]: http://gestionaleamica.com/Backup/
 [2]: http://aws.amazon.com/s3/
