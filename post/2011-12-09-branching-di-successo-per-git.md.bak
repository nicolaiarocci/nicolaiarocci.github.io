---
title: Branching di successo per Git
author: Nicola Iarocci
date: 2011-12-09
url: /branching-di-successo-per-git/
dsq_thread_id:
  - 2043357735
categories:
  - Programming
tags:
  - controllo di versione
  - git
---
<a title="Git" href="http://git-scm.com/" target="_blank">Git</a> è di gran lunga la tecnologia più significativa che il mio team ha introdotto negli ultimi tempi. Grazie a Git la nostra produttività è migliorata a tal punto che davvero non passa giorno senza che mi chieda come abbiamo potuto farne a meno così a lungo.

Git è un <a title="Controllo versione" href="http://it.wikipedia.org/wiki/Controllo_versione" target="_blank">sistema di controllo versione</a> ideato da Linus Torvald (quello di Linux). E&#8217; gratuito, multi-piattaforma, distribuito e soprattutto talmente veloce che sembra aggiungere un pizzico di magia al processo produttivo. Git è una macchina del tempo con cui spostarsi avanti e indietro tra le versioni del codice. E&#8217; l&#8217;ideale sia per progetti individuali che per gruppi di lavoro numerosi e distribuiti. L&#8217;integrità del codice e la preservazione delle versioni sono garantite da un efficiente &#8211; e veloce! &#8211; sistema di _branching_ e _merging_.

Se non avete mai usato prima un sistema di controllo versione (e magari ricorrete ancora a copie manuali del codice tra una release e l&#8217;altra) gioite, perché Git vi cambierà la vita. Se venite da altri sistemi (Subversion, Team Foundation Server) sappiate che Git adotta un approccio fondamentalmente diverso: niente copie differenziali. In Git ogni repository è un mirror integrale della codebase; è quest&#8217;accorgimento ciò che rende Git così veloce. <!--more-->

## Come e dove imparare Git

Git non è difficile, ma richiede un pò d&#8217;impegno iniziale. In rete sono disponibili numerose e ottime fonti. Vi consiglio <a title="Git Pro Book" href="http://progit.org/book/" target="_blank">Git Pro</a>, libro gratuito nella versione online. Stampatelo e tenetelo sempre a portata di mano. Ottimi anche <a title="Git Reference" href="http://gitref.org/" target="_blank">Git Reference</a> e <a title="Everyday GIT" href="http://schacon.github.com/git/everyday.html" target="_blank">Everyday GIT</a> (consigliati dal sito ufficiale), <a title="Git Magic" href="http://www-cs-students.stanford.edu/~blynn/gitmagic/" target="_blank">Git Magic</a> per quando avrete già un pò di dimestichezza con Git, e infine la valida raccolta che trovate su <a title="Stack Overflow" href="http://stackoverflow.com/questions/315911/git-for-beginners-the-definitive-practical-guide?t=1320241886" target="_blank">Stack Overflow</a>.

## La potenza è nulla senza controllo

Uno dei risultati più interessanti che abbiamo ottenuto grazie all&#8217;adozione di Git è la pubblicazione contemporanea di più versioni del nostro <a title="Gestionale Amica" href="http://gestionaleamica.com" target="_blank">software gestionale</a>. C&#8217;è quella ufficiale (stabile) e c&#8217;é quella _sperimentale_ con una anteprima delle novità a cui stiamo ancora lavorando. E&#8217; un pò la nostra _<a title="Neutral Build" href="http://en.wikipedia.org/wiki/Neutral_build" target="_blank">night build</a> e _contiene le cose non ancora mature per affrontare il grande pubblico ma già interessanti per gli utenti più smaliziati. Nel frattempo lavoriamo anche a nuove funzionalità importanti. Queste ultime vedranno la luce solo in occasione dei rilasci più significativi (tipicamente non sono più di due o tre all&#8217;anno) e non sono incluse nelle night build. In tutto questo _bailamme_ di versioni, hotfix e rilasci pubblici e interni non perdiamo una linea di codice e manteniamo i nostri repository allineati, muovendoci avanti e indietro quando necessario.

Per ottenere un risultato così non basta il sistema di controllo versione; è necessaria anche una ottima strategia o, per meglio dire, un modello di branching ben progettato. Dopo diversi tentativi andati più o meno a vuoto la soluzione è arrivata grazie alla scoperta dello spettacolare articolo di <a title="A successful Git branching model" href="http://nvie.com/posts/a-successful-git-branching-model/" target="_blank">Vincent Driessen</a>:

<div id="attachment_4064" style="width: 570px" class="wp-caption aligncenter">
  <a href="http://nvie.com/posts/a-successful-git-branching-model/"><img class="size-full wp-image-4064 " title="Un modello di branching per Git" src="http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/A-successful-Git-branching-model-»-nvie.com_.png?fit=525%2C562" alt="Un modello di branching per Git" srcset="http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/A-successful-Git-branching-model-»-nvie.com_.png?w=560 560w, http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/A-successful-Git-branching-model-»-nvie.com_.png?resize=140%2C150 140w, http://i2.wp.com/nicolaiarocci.com/wp-content/uploads/A-successful-Git-branching-model-»-nvie.com_.png?resize=280%2C300 280w" sizes="(max-width: 525px) 100vw, 525px" data-recalc-dims="1" /></a>
  
  <p class="wp-caption-text">
    Vincent Driessen - Un modello di successo per il branching in Git
  </p>
</div>

Il modello si basa su due branch principali (master e develop) e su tre di supporto (hotfix, feature e release). Lo considero talmente valido che mi sono proposto a Vincent come curatore della traduzione italiana, solo per scoprire che qualcuno prima di me <a title="Modello di branching di Git" href="http://www.diegor.it/it/2010/07/03/howto-il-modello-di-branching-di-git/" target="_blank">ci aveva già pensato</a>: meglio così. Da quando l&#8217;ho scoperto lo applichiamo con zelo e vi consiglio di fare altrettanto, soprattutto se lavorate su progetti complessi.

## Non solo codice

Git è utile anche per i piccoli progetti personali. Anzi, se state cominciando vi consiglio di partire proprio da uno di questi. Non è necessario che sia un programma, potrebbe benissimo trattarsi di un file di testo qualunque. Git funziona con qualunque tipo di file e in effetti viene usato con successo per progetti di scrittura, documentazione, web design e quant&#8217;altro.

Una volta presa dimestichezza con Git non potrete più rinunciarvi, qualunque sia la portata del progetto a cui state lavorando.
