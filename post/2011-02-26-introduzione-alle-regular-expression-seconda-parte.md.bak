---
title: Introduzione alle Regular Expression – Seconda Parte
author: Nicola Iarocci
date: 2011-02-26
url: /introduzione-alle-regular-expression-seconda-parte/
dsq_thread_id:
  - 2017455318
categories:
  - Guide
  - Programming
tags:
  - programmazione
  - regex
  - regular expression
  - tutorial
---
Questa è la seconda parte della serie *Introduzione alle Regular Expression*.
Se non hai ancora letto la [prima parte][1] ti consiglio di farlo. Puoi usare
la <a href="http://regexpal.com/" target="_blank">pagina demo</a> per provare
le query della guida.

## Negazione [^]

Abbiamo già conosciuto la `[cornice]`. Una caratteristica importante di cui non
abbiamo ancora parlato è la negazione. Supponiamo di voler cercare qualunque
carattere *eccetto la lettera a*.

    [^a] # trova b,c,d,e,f,\n .... qualunque carattere eccetto 'a'

La negazione si applica a tutti i caratteri della cornice in cui compare
l'operatore `ˆ`. Non è possibile limitarla a solo alcuni.

    [^0123456789] # trova qualunque carattere non numerico

## Gli Alias

Ora siamo pronti per affrontare qualche esempio realistico di regular
expression. Uno degli usi più frequenti delle regex è la convalida di Stringhe.
Proviamo a verificare la correttezza di un ipotetico numero telefonico da
esprimere nel formato 555-12345678. Di norma divideremmo l'input in due
parti e proveremmo a convertirle in numeri. Ora tuttavia conosciamo le regex
e possiamo sbrigarcela meglio.

    555-[0-9]{7}

Fatto. Stiamo convalidando 555 seguito da un trattino seguito da 7 caratteri
numerici. Possiamo essere addirittura più sintetici, vediamo come.

I range `[0-9]` e `[a-z]`  sono talmente frequenti da saltar fuori continuamente,
tanto che sono state create scorciatoie (alias) dedicate ai range più usati.
Nel nostro caso ci torna utile `\d`, che sta per digit (carattere numerico)
ed è semanticamente identico a `[0-9]`.

    555-\d{7} # identico a 555-[0-9]{7}

Gli alias non sono certo indispensabili, puoi ottenere gli stessi risultati
usando la cornice in modo esteso. Tuttavia sono molto comodi.

<table style="padding: 10px; width: 100%; background-color: #f8f8f8; text-align: left; margin-bottom: 10px;">
  <tr>
    <th>
      alias
    </th>
    
    <th>
      significato
    </th>
    
    <th>
      coorrisponde a
    </th>
  </tr>
  
  <tr>
    <td>
      \d
    </td>
    
    <td>
      digit (numero)
    </td>
    
    <td>
      [0-9]
    </td>
  </tr>
  
  <tr>
    <td>
      \w
    </td>
    
    <td>
      word (parola)
    </td>
    
    <td>
      [a-zA-Z0-9_]  Include il carattere underscore
    </td>
  </tr>
  
  <tr>
    <td>
      \s
    </td>
    
    <td>
      spazio, tab o newline
    </td>
    
    <td>
      [ \t\r\n]
    </td>
  </tr>
  
  <tr>
    <td>
      \D
    </td>
    
    <td>
      qualsiasi non numerico
    </td>
    
    <td>
      ^\d
    </td>
  </tr>
  
  <tr>
    <td>
      \W
    </td>
    
    <td>
      quasiasi non alfanumerico
    </td>
    
    <td>
      ^\w
    </td>
  </tr>
  
  <tr>
    <td>
      \S
    </td>
    
    <td>
      quasiasi ma non lo spazio
    </td>
    
    <td>
      ^\s
    </td>
  </tr>
</table>

**Suggerimento:** nota come ad ogni alias ne corrisponde uno dal significato
opposto, tutto in maiuscolo. Impara i primi tre per conoscerli tutti e sei.

## Il Punto

Il punto è un alias un pò speciale. Ne parlo soprattutto perchè può capitare di
notarlo nel codice scritto da altri. Il punto cerca tutto eccetto il new line
(`\n`). Il problema è che il carattere new line non è lo stesso su tutte le
piattaforme.

    .   # trova tutti i caratteri
    .*  # equivalente a [^\n], trova tutti i paragrafi

Il punto spesso crea confusione. Consiglio di ricorrere a combinazioni di alias
e cornici per ottenere gli stessi risultati senza rischiare errori.

## Escaping

Capita a volte di dover cercare proprio il punto, oppure i caratteri [ o ].
Poiché fanno parte della sintassi regex in questi casi è necessario riccorrere
all'escaping, ovvero precederli col carattere `\` che rappresenta
l'escape. Per esempio

    \.    # cerca il punto invece che tutto quanto
    \*    # trova tutti gli asterischi
    \\    # trova tutti gli escape

## Raggruppamenti e OR

Torniamo alla convalida. Questa volta vogliamo verificare la validità di un
indirizzo email. Prima di tutto stabiliamo le regole (semplificate) a cui una
stringa deve attenersi per venire convalidata come indirizzo email: 1) il nome
utente può contenere lettere, numeri, underscore e trattini ma deve cominciare
con una lettera; 2) il dominio può contenere solo lettere seguite da un punto
seguito da altre lettere. Quindi domain.fakecom è valido per noi

    [a-z][\w-]*@[a-z]+\.[a-z]+

Presta attenzione all'escaping del punto! Un'altro dettaglio
importante è il quantificatore `+` che abbiamo visto nel [primo articolo][1] di
questa serie. Nel dominio infatti vogliamo *almeno* una lettera, non zero
o più.

Supponiamo ora di voler aggiornare le regole in modo da convalidare solo
i domini più importanti. Il nostro indirizzo email deve finire con com oppure
net. Non possiamo risolvere questo problema con quel che abbiamo imparato
finora. La nostra query regex dovrà ricorrere a due nuovi concetti,
l'operatore OR e i gruppi.

    [a-z][\w-]*@[a-z]+\.(com|net)

Vediamo l'OR all'opera

    com|net  #  trova com oppure net
    a|b|c    # lo stesso di [abc].

L'aggiunta delle parentesi () si rende necessaria per chiarire che non
vogliamo trovare _tutte_ le occorrenze della parte di regex alla loro sinistra.
Se volessimo "Brad Pitt" oppure "Angelina Pitt"

    Brad|Angelina Pitt  # trova sia 'Brad' che 'Angelina Pitt'
    (Brad|Angelina) Pitt  # ora ci siamo!

Per un programmatore il concetto del raggruppamento (grouping) con le parentesi
dovrebbe essere facilmente comprensibile. Di fatto possiamo combinarlo con
altri operatori che già conosciamo

    (dog)+   #  trova dog,dogdog,dogdogdog ...
    java(bean)?    #  trova java o javabean

## Conclusione

Questo conclude la seconda parte della guida. La prossima e ultima parte verrà
pubblicata tra qualche giorno. Nel frattempo raccomando di giocare con la <a
href="http://regexpal.com/" target="_blank">pagina demo</a> per fare un
pò di pratica.

E' ora disponibile anche la [terza parte][2] di questo tutorial.

Questo articolo è una traduzione autorizzata di [Regex Primer: Part 2][3]. Ringrazio l'autore per il permesso accordatomi.

 [1]: http://nicolaiarocci.com/introduzione-alle-regular-expression-prima-parte/
 [2]: http://nicolaiarocci.com/introduzione-alle-regular-expression-terza-parte/
 [3]: http://www.agillo.net/regex-primer-part-2/
