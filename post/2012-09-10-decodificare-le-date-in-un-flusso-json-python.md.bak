---
title: Decodificare le date in un flusso JSON (Python)
author: Nicola Iarocci
date: 2012-09-10
url: /decodificare-le-date-in-un-flusso-json-python/
gr_overridden:
  - 1
gr_options:
  - 'a:3:{s:13:"enable-ribbon";s:4:"Show";s:10:"github-url";s:46:"https://github.com/nicolaiarocci/json-datetime";s:11:"ribbon-type";i:5;}'
dsq_thread_id:
  - 2017455636
categories:
  - Programming
tags:
  - datetime
  - json
  - python
---
<a href="https://github.com/nicolaiarocci/json-datetime" title="JSON-Datetime" target="_blank">JSON-Datetime</a> permette di decodificare i valori [cci lang=&#8221;python&#8221; theme=&#8221;default&#8221;]datetime[/cci] normalmente espressi come stringhe in un flusso JSON. E&#8217; davvero molto semplice, e fa parte della suite strumenti open source che sto sviluppando nel contesto del più ampio progetto [RESTful Web API][1].

Del problema della decodifica delle stringhe JSON in valori datetime ho [già scritto in passato][2]. Allora proponevo una soluzione algoritmica; ora vi presento un prodotto finito che potete usare nei vostri progetti.

## Il problema

Lo standard JSON (<a href="http://www.ietf.org/rfc/rfc4627.txt" title="RFC 4627 - JSON standard" target="_blank">RFC 4627</a>) non supporta valori di tipo data/ora. In un flusso JSON le date vengono rappresentate come semplici stringhe che i decoder Python interpretano come tali:

    import simplejson as json
    
    >>>test = '{"name": "John Doe", "born": "Thu, 1 Mar 2012 10:00:49 UTC"}'
    >>>json.loads(test)
    {'name': 'John Doe', 'born': 'Thu, 1 Mar 2012 10:00:49 
    

Nell&#8217;esempio precedente il campo `born` è una stringa nel JSON, e tale rimane dopo la decodifica in un dizionario Python.

## La soluzione

JSON-Datetime è un semplice wrapper attorno al metodo `loads` di <a href="http://simplejson.readthedocs.org/en/latest/index.html#" title="simplejson" target="_blank">simplejson</a>. Ecco che succede quando usiamo JSON-Datetime al posto di simplejson:

    >>> import jsondatetime as json
    >>> test = '{"name": "John Doe", "born": "Thu, 1 Mar 2012 10:00:49 UTC"}'
    
    >>> json.loads(test)
    {'name': 'John Doe', 'born': datetime.datetime(2012, 3, 1, 10, 0 ,49)}
    

Ora `born` assume il valore corretto. Affinché vengano riconosciute, le date contenute nel JSON devono corrispondere a un formato `strptime()` valido indicato con l&#8217;argomento `datetime_format`. Nell&#8217;esempio precedente, poiché l&#8217;argomento è assente, viene usato il valore di default `'%a, %d %b %Y %H:%M:%S UTC'`, corrispondente allo standard RFC 1123 (ex 822). Nell&#8217;esempio che segue usiamo un formato personalizzato:

    >>> import jsondatetime as json
    >>> test = '{"name": "John Doe", "born": "Thu, 1 Mar 2012"}'
    
    >>> json.loads(test, datetime_format="%a, %d %b %Y";)
    {'name': 'John Doe', 'born': datetime.datetime(2012, 3, 1)}
    

JSON-Datetime è un semplice wrapper che ci lascia liberi di usare tutti gli argomenti standard previsti per `loads`, `object_hook` incluso. Ciò significa che questa soluzione (al contrario di quella proposta in precedenza) ci lascia liberi di applicare qualsivoglia parser al nostro flusso JSON.

## Installazione e sorgenti

Per l&#8217;installazione basta il classico `pip install json-datetime`. Il codice è disponibile su <a href="https://github.com/nicolaiarocci/json-datetime" title="JSON-Datetime" target="_blank">GitHub</a>.

 [1]: http://nicolaiarocci.com/sviluppare-una-restful-web-api-con-python-flask-e-mongodb/ "Sviluppare una RESTful Web API"
 [2]: http://nicolaiarocci.com/convertire-una-data-json-in-un-oggetto-datetime-python/ "Convertire una data JSON in un oggetto Python datetime"
