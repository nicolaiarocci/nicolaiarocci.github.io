---
title: Introduzione alle Regular Expression – Prima Parte
author: Nicola Iarocci
date: 2011-02-23
url: /introduzione-alle-regular-expression-prima-parte/
dsq_thread_id:
  - 2017455512
categories:
  - Guide
  - Programming
tags:
  - programmazione
  - regex
  - regular expression
  - tutorial
---
Quando si tratta fare ricerche in blocchi di testo le [**regular
expression**][1] (regex) sono la soluzione ideale. Come programmatore studiare
le regex è stata una delle cose migliori che ho fatto per migliorare la mia
produttività.

  1. Valide in ogni linguaggio e indipendenti dalla piattaforma, le regex sono
     un investimento sempre valido. Java, JavaScript, Ruby, .Net, Python&#8230;
     le regex non cambiano.
  2. Rendono ricerca e sostituzione del testo _enormemente_ più potenti
  3. Soddisfano pienamente il principio [80/20][2]. Basta conoscerne il 20% per
     risolvere l'80% dei problemi.

Ho preparato una <a href="http://regexpal.com/" target="_blank">pagina di
prova</a> per testare le regex del tutorial. In alternativa è sempre possibile
usare una IDE, praticamente tutte supportano le regular expressions.<!--more-->

## Partiamo dalla [cornice]

La regex più semplice? Eccola:

    bank

La quale cerca "bank". Cambiamola leggermente, immaginiamo di voler cercare sia "bank" che "tank" nello stesso blocco di testo.

    [bt]ank  // cerca sia bank che tank

La [cornice] rappresenta comunque 1 carattere. Stiamo ancora cercando una
parola di 4 caratteri, ma il primo può essere "b" oppure "t". I caratteri
inclusi nelle parentesi [] sono legati da una relazione di tipo OR. La loro
posizione è irrilevante, `[tb]ank` è semanticamente identico. Ecco altri esempi
d&#8217;uso della [cornice]:

    [abc]1              // trova a1, b1 o c1
    [cba]1              // trova a1, b1 o c1
    file[0123456789]    // trova file0,file1,file2 ... o file9
    file[0-9]           // trova file0,file1,file2 ... o file9
    [a-z]               // trova a, b, c oppure ... z

Avrai notato che abbiamo introdotto un nuovo operatore. Usando il carattere
`-` definiamo un *range*. Il range ci permette di evitare costrutti
assurdamente lunghi come questo: `[abcdefghijklmnopqrstuvwyz]`. E&#8217; una
scorciatoia.

## Proseguiamo coi Quantificatori

Riprendiamo dall&#8217;esempio iniziale. Immaginiamo di voler trovare *tank*,
*bank*, *tanks*, e *banks*. Potremmo provare in questo modo:

    [bt]anks?

Abbiamo aggiunto il *quantificatore* `?` che agisce sul carattere
che si trova direttamente alla sua sinistra. Significa *una occorrenza oppure
nessuna*, quindi nel nostro caso stiamo dicendo "cerca [bt]ank con una
's' finale o meno". Un quantificatore può essere affiancato a qualunque
carattere e addirittura a una `[cornice]`. Dai una occhiata a questi esempi:

    [bt]anks         // trova banks o tanks
    [bt]anks?        // trova bank, tank, banks oppure tanks
    [bt]?ank         // trova bank, tank oppure ank
    ab?c?            // trova a, ab, abc oppure ac

Riassumendo, quando usiamo un carattere senza quantificatore indichiamo che ne
cerchiamo una singola occorrenza. Quando aggiungiamo un quantificatore cambia
il numero di occorrenze che vogliamo trovare. Nella tabella seguente trovi
l&#8217;elenco dei quantificatori disponibili:

<table style="width: 100%; background-color: #f8f8f8; padding: 10px; text-align: left; margin-bottom: 10px;">
  <tr>
    <th>
      quantificatore
    </th>
    
    <th>
      significato
    </th>
    
    <th>
      regex
    </th>
    
    <th>
      esempio
    </th>
  </tr>

  <tr>
    <td>
      ?
    </td>
    
    <td>
      zero o 1
    </td>
    
    <td>
      abc?
    </td>
    
    <td>
      ab, abc
    </td>
  </tr>

  <tr>
    <td>
      *
    </td>
    
    <td>
      zero o più
    </td>
    
    <td>
      abc*
    </td>
    
    <td>
      ab,abc,abcc,abccc,abcccc,… etc
    </td>
  </tr>

  <tr>
    <td>
      +
    </td>
    
    <td>
      uno o più
    </td>
    
    <td>
      abc+
    </td>
    
    <td>
      abc,abcc,abccc,abcccc,…etc
    </td>
  </tr>

  <tr>
    <td>
      {n}
    </td>
    
    <td>
      esattamente n volte
    </td>
    
    <td>
      abc{2}
    </td>
    
    <td>
      abcc
    </td>
  </tr>

  <tr>
    <td>
      {n,m}
    </td>
    
    <td>
      da n a m volte
    </td>
    
    <td>
      abc{2,3}
    </td>
    
    <td>
      abcc,abccc
    </td>
  </tr>
</table>

## Concludendo

Abbiamo appreso la sintassi base che ci consente di fare un pò di pratica.
E&#8217; una buona idea fare quale esperimento in una IDE oppure sulla <a
href="http://regexpal.com/" target="_blank">pagina demo</a>.

La seconda parte di questa guida è ora [pubblicata][3].

Questo articolo è una traduzione autorizzata di [Regex Primer: Part 1][4].
Ringrazio l&#8217;autore per il permesso accordatomi.

 [1]: http://it.wikipedia.org/wiki/Espressione_regolare
 [2]: http://en.wikipedia.org/wiki/Pareto_principle#In_software
 [3]: http://nicolaiarocci.com/introduzione-alle-regular-expression-seconda-parte/
 [4]: http://www.agillo.net/regex-primer-part-1/
