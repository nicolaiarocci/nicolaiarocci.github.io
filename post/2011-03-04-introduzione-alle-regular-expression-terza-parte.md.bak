---
title: Introduzione alle Regular Expression – Terza Parte
author: Nicola Iarocci
date: 2011-03-03
url: /introduzione-alle-regular-expression-terza-parte/
dsq_thread_id:
  - 2017455233
categories:
  - Guide
  - Programming
tags:
  - programmazione
  - regex
  - regular expression
  - tutorial
---
Benvenuto alla terza e ultima parte della nostra *Introduzione alle Regular
Expression*. Concluso il capitolo sarai  in grado di affrontare la maggior
parte dei problemi di ricerca nel testo. Se ancora non l'hai fatto ti
consiglio di leggere la [Prima Parte][1] e la [Seconda Parte][2]. Ricorda che
puoi usare la <a href="http://regexpal.com/" target="_blank">pagina di
prova</a> per testare le query della guida.

## Avidità

Il problema della avidità degli operatori regex diventa evidente quando si
comincia a lavorare su ricerche avanzate. Un caso tipico è il parsing di file
XML o HTML.

    <p>questo è un <b>paragrafo</b></p>

Supponiamo di voler trovare tutti i tag usati.

    <.*> # cerca tutti i tag

Il risultato della query non è quello che ci si potrebbe aspettare.
L'operatore `*` è *avido*, ovvero cerca di catturare più caratteri
possibili. Una volta trovato il primo `<` prosegue avidamente selezionando tutto
fino all'ultimo `>`. In questo caso vogliamo che si fermi al primo `>`, non
all'ultimo. E' questa una distinzione importante, da comprendere
a fondo. Possiamo disattivare il comportamento avido aggiungendo il carattere?

    <.*?> # ora otteniamo quel che vogliamo (niente avidità)

Se desideriamo usare l'operatore `+` (1 o più) al posto del `*` (zero o più),
la nostra query diventa `<.+?>`.

## Confini

Nella [seconda parte][2] del nostro tutorial abbiamo convalidato un numero
telefonico nel formato 555-12345678

    555-\d{8}   # 555- seguito da 8 cifre

Anche se tecnicamente corretta questa query non è perfetta. Se la testiamo con
queste stringhe:

    testoDavanti 555-12345678
    555-12345678 il mio telefono

scopriamo che vengono accettate perché la regola `555-\d{8}` è ancora valida.
In realtà noi desideriamo accettare il solo il numero telefonico, niente
altro. La soluzione richiede l'uso degli operatori di confine:

    ^555-\d{8}$

I confini sono caratteri speciali perché non occupano spazio. Sono dei
segnaposto che servono a delimitare il testo da cercare. Dopo l'inizio
`(^)` deve esserci il nostro numero di telefono; prima della fine `($)` deve
esserci il nostro numero di telefono.

<table style="padding: 10px; width: 100%; background-color: #f8f8f8; text-align: left; margin-bottom: 10px;">
  <tr>
    <th>
      confine
    </th>
    
    <th>
      significato
    </th>
  </tr>
  
  <tr>
    <td style="vertical-align: top;">
      ^
    </td>
    
    <td style="vertical-align: top;">
      Inizio del testo. Sfortunatamente gli inventori di regex hanno scelto lo stesso carattere usato per la negazione. E&#8217; importante riconoscerne il significato in base al contesto. Quando non è compreso tra [ e ] il carattere ^ è un confine e indica l&#8217;inizio del testo.
    </td>
  </tr>
  
  <tr>
    <td>
      $
    </td>
    
    <td>
      fine del testo
    </td>
  </tr>
</table>

Quindi

    a   #  trova qualunque a
    ^a  #  trova solo il testo che comincia per a
    a$  #  trova solo il testo che finisce per a

C'è un altro confine, quello di parola `(\b)`. Vediamo un esempio. Vogliamo
cercare le parole "for" e "she" nella nostra <a href="http://regexpal.com/"
target="_blank">pagina di test</a>.

    (for|she)  # trova for e she

Non va male. Trova tutte le occorrenze di "she" e "for", tuttavia viene
selezionata anche la parola "before". Non è il comportamento desiderato.
Potremmo tentare cercando solo le occorrenze precedute e succedute da uno
spazio.

    [ ](for|she)[ ]  # cerca for o she

Va meglio. Non seleziona più before. Abbiamo però un nuovo problema. Nel testo
c'è la frase "for she had plenty of time". La nostra regex non ha individuato
la parola "she" contenuta nella frase. Per quale motivo?

    for she had plenty of time

Con il "for" iniziale abbiamo già rintracciato lo spazio che precede "she", che
quindi viene escluso. Sono queste le situazioni un cui un confine di parola può
risolvere il problema.

    \b(for|she)\b  # trova she oppure for

Il confine `\b` definisce dove la parola comincia e finisce, proprio come
succede con i confini visti prima. Abbiamo detto prima che i "confini non
occupano spazio". Nell'esempio qui sopra cerchiamo esattamente
"for" o "she". Non cerchiamo la stringa `\b` e questa non occupa alcuno spazio
durante la ricerca, a differenza di quel che è successo quando abbiamo tentato
di usare la `[cornice]`. E' un dettaglio importate perché con tutti gli
altri operatori regex ciò che è nella query "occupa spazio" e non
può essere trovato *di nuovo*.

## Il Finale: Ricerca e Sostituzione

Ce l'hai fatta! Sei arrivato in fondo. Congratulazioni. Il meglio arriva ora.
Ricerca e sostituzione è senz'altro il mio argomento preferito. Qui la pagina
di test non ci può aiutare, occorre qualche tipo di editor oppure una IDE
(Eclipse/Notepad++/Wordpad).

Supponiamo di avere un file composto da 100 righe come queste

    31-01-10_backup32
    24-01-10_backup1
    24-02-10_backup_mona
    11-03-09_backup_lisa

Vogliamo correggere le date portandole dal formato europeo a quello americano
(da `gg-mm-aa` a `mm-gg-aaaa`).

    \d{2}-\d{2}-\d{2}_backup.*  // trova le nostre righe

Per ogni riga desideriamo sostituire aree specifiche quindi ricorriamo
all'operatore di raggruppamento già visto nella [seconda parte][2] di
questa guida.

    (\d{2})-(\d{2})-(\d{2})_backup(.*)  // ci siamo

A questo punto tutto quel che dobbiamo fare è sostituire le righe trovate con

<span style="color: #ff0000;">{Gruppo2}</span>&#8211;<span style="color: #ff0000;">{Gruppo1}</span>-20<span style="color: #ff0000;">{Gruppo3}</span>_backup<span style="color: #ff0000;">{Gruppo4}</span>

Il che si traduce nella seguente espressione di sostituzione

    \2-\1-20\3_backup\4

Facile no? Niente più lavori ripetitivi. La mia regola è: se un testo richiede
la modifica di più di cinque righe è giunta l'ora di ricorrere alle
regex. Potrebbe sembrare una esagerazione. Eppure un programmatore dovrebbe
rifiutarsi per principio di ripetere manualmente un lavoro che può essere
automatizzato.

Buona fortuna.

Questo articolo è una traduzione autorizzata di [Regex Primer: Part 3][3].
Ringrazio l'autore per il permesso accordatomi.

 [1]: http://nicolaiarocci.com/introduzione-alle-regular-expression-prima-parte/
 [2]: http://nicolaiarocci.com/introduzione-alle-regular-expression-seconda-parte/
 [3]: http://www.agillo.net/regex-primer-part-3/
