---
title: Convertire una data JSON in un oggetto datetime Python
author: Nicola Iarocci
date: 2012-06-07
url: /convertire-una-data-json-in-un-oggetto-datetime-python/
dsq_thread_id:
  - 2017455452
categories:
  - Programming
tags:
  - datetime
  - json
  - programmazione
  - python
---
Abbiamo una stringa JSON che contiene una data:

    fonte = '{"ragione_sociale": "CIR 2000", "aggiornato_il": "Wed, 06 Jun 2012 14:19:53 UTC"}'
    

Vediamo che succede se la convertiamo in un dizionario Python:

    import simplejson as json
    
    json.loads(fonte)
    {'aggiornato_il': 'Wed, 06 Jun 2012 14:19:53 UTC ', 'ragione_sociale': 'CIR 2000'}
    

Facile, vero? C&#8217;è però un piccolo problema: `aggiornato_il` è ancora una stringa mentre a noi, per poterlo elaborare comodamente, serve un campo `datetime.datetime`. Come mai il pur potente modulo `simplejson` non converte correttamente la nostra data?

## Il problema

Il fatto è che il JSON originale non fa nulla per informarci del fatto che il campo `aggiornato_il` esprime in realtà una data. La radice del problema sta nello standard JSON il quale non contempla la dichiarazione esplicita dei tipi di dati. In effetti la stessa questione si pone nella conversione di un numero non intero: va considerato un float, oppure un decimal? In quest&#8217;ultimo caso `simplejson` ci viene in aiuto con il parametro parse_float:

    import simplejson as json
    
    json.loads('1.1', parse_float=decimal.Decimal)
    Decimal('1.1')
    

Purtroppo, per il motivo visto prima, non esiste un equivalente per le date.

## La soluzione classica

In questi casi la prassi comune è rendere esplicito, già all&#8217;interno della stringa JSON, il formato del campo. Qualcosa del genere:

    {"aggiornato_il": "$date: Wed, 06 Jun 2012 14:19:53 UTC"}
    

Così facendo possiamo in seguito manipolare il dizionario restituito dal metodo `loads`: intercettare la direttiva `$date` e sostituire finalmente la stringa con una data. Una soluzione più raffinata è quella di sfruttare l&#8217;opzione `object_hook` che consente di invocare una nostra funzione ad ogni chiamata del metodo `loads`.

## La mia soluzione

Nel mio caso il provider JSON è esterno, e non desidero obbligarlo a pre-processare le stringhe JSON inserendo clausole $date arbitrarie solo per soddisfare le esigenze della mia applicazione. Sfruttando l&#8217;opzione object_hook già accennata ho ottenuto una soluzione del tutto trasparente:

    fonte = '{"aggiornato_il": "Thu, 1 Mar 2012 10:00:49 UTC"}'
    dct = json.loads(fonte, object_hook=datetime_parser)
    dct
    {u'aggiornato_il': datetime.datetime(2012, 3, 1, 10, 0, 49)}
    
    
    def datetime_parser(dct):
        for k, v in dct.items():
            if isinstance(v, basestring) and re.search(" UTC", v):
                try:
                    dct[k] = datetime.datetime.strptime(v, DATE_FORMAT)
                except:
                    pass
        return dct
    

La funzione `datetime_parser` esamina gli elementi della stringa JSON. In caso di corrispondenza alla espressione regolare indicata in `re.search` tentiamo una conversione diretta al formato `datetime`. Data la specificità della espressione regolare la conversione dovrebbe avere successo. Il blocco `try... except` ci permette di ignorare un eventuale errore: in questo caso infatti presumiamo che si tratti di una stringa vera e propria e non, malgrado la somiglianza, di una data. L&#8217;unico vincolo imposto al provider JSON è l&#8217;adozione di un formato standard per rappresentare le date. Nel mio caso è il seguente:

    DATE_FORMAT = '%a, %d %b %Y %H:%M:%S UTC'
    

Per approfondimenti vi consiglio:

  * <a title="JSON encoder and decoder" href="http://docs.python.org/library/json.html" target="_blank">JSON econdoer and decoder</a>
  * [Introduzione alle Regular Expression][1]

Per completezza c&#8217;è da aggiungere che l&#8217;adozione di un <a title="json schema" href="http://www.google.it/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=0CGgQFjAA&url=http%3A%2F%2Fjson-schema.org%2F&ei=-GrQT_rzHYbHsgb9ob36DQ&usg=AFQjCNE-i8CJOQfjyG2n0It-nN20sJ-cZg" target="_blank">json schema</a> consentirebbe la specifica dei tipi di dati JSON. Quest&#8217;ultima soluzione però, data la sua complessità, non è applicabile nel mio e in molti altri casi.

PS: ne ho scritto anche su <a title="How to convert a python datetime object with json loads" href="http://stackoverflow.com/questions/8793448/how-to-convert-to-a-python-datetime-object-with-json-loads/10734224#10734224" target="_blank">Stack Overflow</a>.

 [1]: http://nicolaiarocci.com/introduzione-alle-regular-expression-prima-parte/ "Introduzione alle Regular Expression"
