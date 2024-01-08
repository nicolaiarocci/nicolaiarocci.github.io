---
title: Usare Git con Dropbox
author: Nicola Iarocci
date: 2012-03-17
url: /usare-git-con-dropbox/
dsq_thread_id:
  - 2022843041
categories:
  - Programming
tags:
  - dropbox
  - git
  - programmazione
---
<p style="text-align: left;">
  Lavorando con <a title="Branching di successo per Git" href="http://nicolaiarocci.com/branching-di-successo-per-git/">Git</a> si può sentire l&#8217;esigenza di un repository privato e condiviso tra diversi computer. Se non volete spendere soldi <a title="GitHub" href="https://github.com/" target="_blank">GitHub</a> non è un&#8217;opzione dato che i suoi repo privati sono a pagamento. L&#8217;alternativa naturale è <a title="BitBucket" href="https://bitbucket.org/" target="_blank">BitBucket</a>, che da qualche tempo supporta Git e consente la creazione gratuita di repository privati.
</p>

## Usare Dropbox come repository Git remoto

Recentemente, più che altro per curiosità, ho giocato con una terza opzione: <a title="Dropbox" href="http://db.tt/V8L8FFo" target="_blank">Dropbox</a>. Per me Dropbox è uno strumento indispensabile sia per il lavoro che per le mie cose personali. Su qualunque computer io sia, ovunque mi trovi, grazie a Dropbox ho accesso al mio materiale. Dunque, mi son detto, perché non usarlo anche per il codice,  pur senza rinunciare al controllo versione offerto da Git?

[<img style="border-style: initial; border-color: initial; border-image: initial; border-width: 0px;" title="Dropbox" src="/images/dropbox.png?resize=525%2C131" alt="Dropbox" data-recalc-dims="1" />][1]

Ebbene ho scoperto che non solo è possibile, è anche molto semplice. In realtà non c&#8217;è nulla di nuovo in quel che vi mostro, la &#8216;magia&#8217; la fa tutta Dropbox. <!--more-->

## Creare un Git repository &#8216;remoto&#8217; su Drobox

Se siete su Linux o Mac aprite una finestra terminale; su Windows aprite semplicemente Git Bash. Se avete una installazione predefinita la cartella Dropbox si trova nella HOME di Linux e Mac, oppure nella Documenti di Windows.

Spostatevi nella cartella Dropbox:

<pre class="brush:shell">cd ~
cd Dropbox</pre>

Una volta entrati in ~/Dropbox create un &#8216;bare&#8217; repository:

<pre class="brush:shell">mkdir progetto1
cd progetto1
git --bare init</pre>

Il nostro repository privato, l&#8217;equivalente di un repo remoto alla GitHub per capirci, è pronto. Lo useremo per tenere sincronizzati i nostri computer. Naturalmente appoggiarci a Dropbox ci garantisce anche la possibilità di ricorrere a un restore di emergenza nel caso il codice venga perduto localmente.

## Creare il Git repository locale

Su ognuno dei computer creiamo il repository locale:

<pre class="brush:shell">cd ~
mkdir progetto1
cd progetto1
git init</pre>

Lavoriamo un po&#8217;, quindi facciamo la nostra commit locale:

<pre class="brush:shell">touch testo1.txt testo2.txt test.py
echo "aggiungo del testo a testo" &gt; testo1.txt

git add *
git commit -m 'commit iniziale'</pre>

Ora colleghiamo il repo &#8220;remoto&#8221; (quello in Dropbox) al nostro repository locale:

<pre class="brush:shell">git remote add origin ~/Dropbox/progetto1</pre>

Ora possiamo fare il push verso il remoto dei files locali. Dal branch [cci lang=&#8221;bash&#8221; theme=&#8221;default&#8221;]master[/cci] verso [cci lang=&#8221;bash&#8221; theme=&#8221;default&#8221;]origin[/cci]:

<pre class="brush:shell">git push origin master</pre>

Fatto! Possiamo simulare facilmente il lavoro su un&#8217;altro computer. Basta clonare [cci lang=&#8221;bash&#8221; theme=&#8221;default&#8221;]progetto[/cci] dal &#8216;remoto&#8217;, cambiare qualche file e salvarlo:

<pre class="brush:shell">cd ~
git clone ~/Dropbox/progetto1 test_clone
cd test_clone
ls &gt; testo2.txt
git commit testo2.txt -m 'qualche modifica'
git push origin master</pre>

Torniamo ora al folder locale originale. Possiamo sincronizzarlo e aggiornarlo con le modifiche fatte sul &#8220;secondo computer&#8221;:

<pre class="brush:shell">cd ~
cd progetto1
git pull origin master</pre>

## Il versioning di Dropbox

Dropbox è dotato di un proprio sistema di versioning, pertanto aggiungere Git potrebbe sembrare superfluo. Qualunque sviluppatore avvezzo a Git vi dirà che non è così. Il versioning di Dropbox è adatto a file di testo, fogli di calcolo, immagini e quant&#8217;altro ma non ha niente a che vedere con le capacità di manutenzione e gestione dei progetti offerte da Git.

## Git e Dropbox per gruppi di lavoro?

E&#8217; sufficiente condividere il folder Dropbox con altre persone per creare un ambiente di sviluppo privato ma condiviso col proprio gruppo di lavoro. In quest&#8217;ultimo caso la probabilità di conflitti aumenta notevolmente. Si tratta di una soluzione forse interessante per mini-team di 2 o 3 persone nei quali è relativamente facile evitare la generazione di conflitti (evitare le push contemporanee).

## Concludendo

BitBucket o GitHub (a pagamento) rimangono la soluzione ideale, e offrono molte funzionalità comunque assenti in Git+Dropbox (interfaccia web, wiki, issues, eccetera). Per piccoli progetti personali Dropbox offre una alternativa a buon mercato, rapida e comoda.

*PS: se create un account Dropbox dal link dell&#8217;articolo, oppure da <a href="http://db.tt/V8L8FFo" title="Dropbox" target="_blank">questo</a>, ricevete 500BMB extra (e altrettanti ne otterrà il sottoscritto)!*

 [1]: http://db.tt/V8L8FFo
