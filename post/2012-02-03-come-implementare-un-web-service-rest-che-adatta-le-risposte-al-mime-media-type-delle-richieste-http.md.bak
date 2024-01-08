---
title: Una REST API che adatta le sue risposte al MIME Media-Type delle richieste HTTP
author: Nicola Iarocci
date: 2012-02-03
url: /come-implementare-un-web-service-rest-che-adatta-le-risposte-al-mime-media-type-delle-richieste-http/
gr_overridden:
  - 1
gr_options:
  - 'a:3:{s:13:"enable-ribbon";s:4:"Show";s:10:"github-url";s:49:"https://github.com/nicolaiarocci/flask-mimerender";s:11:"ribbon-type";s:1:"5";}'
dsq_thread_id:
  - 2109650542
categories:
  - Programming
tags:
  - flask
  - programmazione
  - python
  - rest api
---
Da qualche tempo sto lavorando alla implementazione di una REST API. In linea generale e semplificando, una <a title="Application programming interface" href="http://it.wikipedia.org/wiki/Application_programming_interface" target="_blank">API</a> è un servizio che espone alcune funzionalità, è accessibile via internet più o meno liberamente ed è, infine, utilizzabile non solo da persone fisiche ma anche e soprattutto da altre applicazioni. Un esempio di API è quella di Facebook, che consente a chiunque di creare applicazioni che interagiscono con gli utenti e le pagine Facebook. Già, se non ci fosse la API non esisterebbero i terribili giochini Facebook&#8230;

Una delle specifiche <a title="REST" href="http://it.wikipedia.org/wiki/Representational_State_Transfer" target="_blank">REST</a> più importanti vuole che un servizio RESTful sia in grado di fornire dati in più formati, in modo tale da soddisfare il maggior numero possibile di utenti/applicazioni. Immaginiamo un servizio che fornisce i risultati delle partite del campionato di calcio. Supponiamo che arrivino tre richieste successive per lo stesso risultato: la prima potrebbe chiedere una risposta in formato XML, la seconda in JSON e la terza in HTML. Il  nostro servizio deve rispondere a tutte e tre le richieste, adattando il flusso di dati della risposta al formato di ognuna.

<img class="alignright size-full wp-image-4402" style="border-style: initial; border-color: initial; border-image: initial; border-width: 0px;" title="Flask" src="http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/flask.png?fit=300%2C117" alt="Flask" srcset="http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/flask.png?w=300 300w, http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/flask.png?resize=150%2C58 150w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" />Nel mio caso la API che sto implementando supporta XML, JSON, HTML e testo puro. E&#8217; scritta in Python (ma va!) e si appoggia all&#8217;eccellente <a title="Flask" href="http://flask.pocoo.org/" target="_blank">Flask</a> micro web framework. Per risolvere in maniera elegante il problema delle risposte multi-formato ho deciso di usare i <a title="Python Decorators" href="http://www.python.org/dev/peps/pep-0318/" target="_blank">decorator</a>, una delle caratteristiche più interessanti di Python. Dopo un po&#8217; di lavoro in proprio ho scoperto che qualcuno aveva già risolto il problema, per giunta con la stessa tecnica. <a title="mimerender" href="http://code.google.com/p/mimerender/" target="_blank">MimeRender</a> di Martin Blech è un&#8217;ottima soluzione, solo che è specifica per web.py (un altro web framework). La mia soluzione non disponeva di alcune opzioni interessanti che MimeRender include; ho deciso allora di scrivere un port di MimeRender per Flask, e di metterlo a disposizione del pubblico.<!--more-->

## Istruzioni per l&#8217;uso

Prima di tutto è necessario fornire le funzioni da usare per il rendering, una per ogni formato che intendiamo supportare:

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/1730305">Gist</a>.
  </noscript>
</div>

Quindi decoriamo la nostra funzione, definendo per lei la mappa delle funzioni di rendering:

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/1730312">Gist</a>.
  </noscript>
</div>

Tutto qui! In caso di richiesta GET la funzione `index` restituisce un dizionario, il quale verrà reso da MimeRender come XML, JSON o quant&#8217;altro, a seconda del Content-Type specificato nella richiesta HTTP:

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/1729566">Gist</a>.
  </noscript>
</div>

Su <a title="Flask MimeRender" href="https://github.com/nicolaiarocci/flask-mimerender" target="_blank">github </a>trovate l&#8217;esempio completo nonché il codice sorgente del renderer, che potete scaricare liberamente.
