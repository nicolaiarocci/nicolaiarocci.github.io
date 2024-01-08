---
title: Il Cloud Computing è davvero affidabile?
author: Nicola Iarocci
date: 2011-06-03
url: /il-cloud-computing-e-davvero-affidabile/
dsq_thread_id:
  - 2039195180
categories:
  - Programming
tags:
  - api
  - cloud
  - cloud computing
  - programmazione
  - web
---
<img class="alignright size-medium wp-image-2755" title="Cloud Computing" src="images/cloud-computing-300x214.jpg?w=200" alt="Cloud Computing" srcset="http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/cloud-computing.jpg?resize=300%2C214 300w, http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/cloud-computing.jpg?resize=150%2C107 150w, http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/cloud-computing.jpg?resize=420%2C300 420w, http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/cloud-computing.jpg?w=559 559w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" />E&#8217; di pochi giorni fa la <a title="Spring cleaning for some of our APIs" href="http://googlecode.blogspot.com/2011/05/spring-cleaning-for-some-of-our-apis.html" target="_blank">notizia</a> che alcuni servizi API gratuiti forniti da Google verranno chiusi. Tra questi spicca **<a title="Google Translate API" href="http://code.google.com/intl/it-IT/apis/language/translate/overview.html" target="_blank">Translate API</a>**, la più apprezzata libreria gratuita per la traduzione automatica sul web. Basta una occhiata ai <a href="http://googlecode.blogspot.com/2011/05/spring-cleaning-for-some-of-our-apis.html#comments" target="_blank">commenti </a>per rendersi conto dello sconcerto generato dall&#8217;annuncio, per altro del tutto inatteso. Molti si dicono disposti a pagare pur di non rinunciare alla API, ma non è  questa l&#8217;idea di Google che in alternativa propone <a title="Google Translate Element" href="http://www.google.com/webelements/#!/translate" target="_blank">Google Translate Element</a>, widget gratuito che certo non è una soluzione accettabile per applicazioni che attualmente integrano la API in maniera trasparente. Immagino che proprio qui stia il nocciolo della questione: una API non è visibile né apprezzabile dall&#8217;esterno, mentre un widget promuove il brand Google.

Migliaia di aziende, enti pubblici e organizzazioni non governative internazionali che oggi usano la API dovranno trovare soluzioni alternative, probabilmente a pagamento. Almeno gli è stato concesso un po&#8217; di tempo: Google garantisce un periodo di tre anni prima della sospensione del servizio.

<img class="aligncenter size-full wp-image-2776" title="Translate API Deprecata" src="http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/TranslateAPI.png?fit=480%2C82" alt="Translate API Deprecata" srcset="http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/TranslateAPI.png?w=480 480w, http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/TranslateAPI.png?resize=150%2C25 150w, http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/TranslateAPI.png?resize=300%2C51 300w" sizes="(max-width: 480px) 100vw, 480px" data-recalc-dims="1" />

Questa notizia induce ancora una volta alcune riflessioni circa l&#8217;affidabilità del **<a title="Cloud Computing" href="http://it.wikipedia.org/wiki/Cloud_computing" target="_blank">Cloud Computing</a>**, modello di sviluppo verso il quale, volenti o nolenti, tutti noi siamo diretti. <!--more-->

<span style="font-size: 20px; font-weight: bold;">Stand-Alone Vs Cloud Computing</span>

Le vecchie applicazioni stand alone funzionano sempre e comunque. Prima o poi il programmatore originale sparisce dalla circolazione; del codice sorgente (se disponibile) nessuno capisce più nulla, ma l&#8217;applicazione continua a girare. E se una delle librerie usate dall&#8217;applicazione (le vecchie .dll, per capirci) viene improvvisamente abbandonata dal produttore? Non ci sono problemi, l&#8217;installazione gira come prima.

Nel dorato mondo <a title="SaaS - Platform As A Service" href="http://en.wikipedia.org/wiki/Platform_as_a_service" target="_blank">PaaS</a> le applicazioni smettono di funzionare non appena una singola API remota diventa inaccessibile. Non mi sembra una differenza da poco.

## Disservizi e sorprese

Si potrebbe obiettare che appoggiarsi a una API gratuita per sviluppare un prodotto strategico non è una mossa intelligente e che comunque casi di disservizi come questo sono assai rari. In Aprile alcuni server Amazon AWS (la piattaforma cloud più usata al mondo) <a href="http://www.informationweek.com/news/cloud-computing/infrastructure/229402054" target="_blank">sono andati in corto circuito</a> lasciando improvvisamente a piedi centinaia di fornitori di servizi e diversi milioni di loro utenti. Il disservizio, durato oltre ventiquattro ore, è avvenuto nonostante AWS sia un servizio a pagamento di altissimo livello che garantisce un livello di Service Level Agreement (SLA) superiore al 99%.

Un caso diverso ma dalle stesse conseguenze  si è verificato proprio in casa Google poche settimane fa, quando <a title="Google App Engine" href="http://code.google.com/intl/it-IT/appengine/" target="_blank">Google App Engine</a> è diventato a pagamento (almeno per alcuni livelli di utilizzo prima gratuiti), mettendo di fatto fuori mercato molti piccoli servizi gratuiti che avevano scelto la piattaforma cloud del gigante di Mountain View.

## Le contromisure necessarie

Non per questo penso che il cloud computing vada evitato, ne sono anzi un sostenitore convinto, ma è importante per noi tutti **comprendere a fondo i limiti e i rischi che questo nuovo paradigma porta con sé**.

Un paio di anni fa ho scritto <a title="Amica Prodigy Backup" href="http://gestionaleamica.com/Backup/" target="_blank">un programma di backup remoto</a> che si appoggia a <a title="Amazon S3" href="http://aws.amazon.com/s3/" target="_blank">Simple Storage Service</a> (S3), uno dei servizi della piattaforma Amazon AWS. Il programma ha continuato a lavorare impunemente mentre il disastro si abbatteva sui server Amazon della East Coast perché, fin dall&#8217;inizio, era progettato per far fronte a evenienze come questa. Usa server multipli ridondanti dislocati su più aree geografiche, in modo che il crash di una singola server farm non lo mandi in tilt. E&#8217; bene aspettarsi il peggio dai servizi cloud per essere pronti a gestire la crisi se (quando) verrà.

Per quanto riguarda il modello di business, è necessario adottarne uno che garantisca margini sufficienti a compensare improvvisi aumenti delle tariffe, anche solo per il periodo necessario alla eventuale dislocazione. La tendenza generale del mercato è comunque rassicurante: in questi anni costi dei servizi cloud sono calati costantemente.

## Le responsabilità stanno da entrambe le parti

E se domani mi si annunciasse che S3 è improvvisamente deprecato? Fortunatamente per me e per le migliaia di altri il servizio non è gratuito e assicura ad Amazon utili stellari, ma non è questo il punto. Il punto è che in ogni momento _potrebbe succedere_.

I fornitori di servizi cloud hanno una grande responsabilità: garantire la continuità del loro servizio anche e soprattutto nel lungo periodo. Speriamo che ne siano coscienti. Noi programmatori e analisti dobbiamo tenere conto dei rischi che corriamo quando scegliamo di lavorare su piattaforme cloud, progettando i nostri prodotti di conseguenza.

_Aggiornamento. Venerdì 3 giugno Google ha ritoccato l&#8217;annuncio ufficiale. La chiusura è annullata e la Translate API verrà messa a pagamento._
