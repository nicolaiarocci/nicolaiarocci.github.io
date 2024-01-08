---
title: Come annullare una Commit in Git
author: Nicola Iarocci
date: 2012-05-17
url: /come-annullare-una-commit-in-git/
dsq_thread_id:
  - 2017455675
categories:
  - Programming
tags:
  - git
  - programmazione
---
<img class="alignright size-thumbnail wp-image-4967" style="border-style: initial; border-color: initial; border-image: initial; border-width: 0px;" title="Git Logo" src="http://i0.wp.com/nicolaiarocci.com/wp-content/uploads/gitlogo-150x62.png?fit=150%2C62" alt="Git Logo" srcset="images/gitlogo.png?resize=150%2C62 150w, http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/gitlogo.png?resize=300%2C125 300w, http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/gitlogo.png?resize=500%2C208 500w, http://i1.wp.com/nicolaiarocci.com/wp-content/uploads/gitlogo.png?w=910 910w" sizes="(max-width: 150px) 100vw, 150px" data-recalc-dims="1" />Usando <a title="Git" href="http://git-scm.com/" target="_blank">Git</a> capita ogni tanto, vuoi per stanchezza o per distrazione, di lanciare commit sbagliate. Stamattina m&#8217;è capitato di sistemare del codice, testarlo e fare la commit&#8230; solo per scoprire di aver lavorato sulla branch sbagliata! Non è la prima volta che mi succede e non sarà nemmeno l&#8217;ultima. Poiché ho scarsa memoria ogni volta mi tocca usare google e ripescare quei due o tre comandi utili in questi casi. Ho pensato di appuntarli qui, un po&#8217; per metterli a disposizione di tutti, un po&#8217; per poterli ritrovare facilmente. <!--more-->

## Annullare una commit

Se ancora non è stato stato eseguito il push verso un repo remoto:

<pre>git reset --soft HEAD^
</pre>

In Git `HEAD` è la commit più recente mentre `HEAD^` è la penultima (`HEAD^^` è la terzultima). In alternativa è possibile indicare l&#8217;SHA-1 dell&#8217;hash della commit alla quale si vuole tornare, qualunque essa sia:

<pre>git reset --soft 9fa5f6a
</pre>

Il numero di hash di ogni commit è rintracciabile con un semplice `git log --oneline`

## Differenza tra `--soft` e `--hard`

L&#8217;opzione `--soft` cancella la commit ma lascia i file invariati. Se volete riportare anche i file allo stato in cui si trovavano alla penultima commit:

<pre>git reset --hard HEAD^
</pre>

Questo porterà &#8220;indietro nel tempo&#8221; il vostro repo, alla penultima commit. Sarà come se le ultime modifiche (e con esse l&#8217;ultima commit) non fossero mai esistite.

## E se la commit è già finita nel repository?

Se la commit è già stata inviata a un repo remoto (push) è necessario seguire un&#8217;altra procedura:

<pre>git revert HEAD
</pre>

Questo comando crea una _nuova commit_ che annulla tutto ciò che è stato introdotto dalla commit indesiderata.
