---
title: Impara Python in 10 minuti
author: Nicola Iarocci
date: 2011-03-10
url: /impara-python-in-10-minuti/
share: false
dsq_thread_id:
  - 2017454648
categories:
  - Guide
  - Programming
tags:
  - python
  - tutorial
---

E così vorresti imparare il linguaggio di programmazione Python. Probabilmente
sei alla ricerca di un tutorial completo e allo stesso tempo conciso. Questa
guida è un tentativo di insegnarti Python in 10 minuti. In effetti più che con
una guida vera e propria hai a che fare con degli appunti che userai per
partire col piede giusto. Naturalmente se davvero vuoi imparare bene dovrai
anche esercitarti molto. Do per scontato che tu sappia già programmare, questo
mi permetterà di concentrarmi sulle caratteristiche intrinseche del linguaggio.
Troverai le parole chiave *evidenziate* così potrai individuarle facilmente.
*Fai attenzione* perché per brevità alcune cose verranno introdotte
e commentate direttamente nel codice di esempio.

### Attribuzione

Questo articolo è una traduzione autorizzata di [Learn Python in 10
minutes][1]. Ringrazio l'amico Stavros Korokithakis per il permesso
di accordatomi.

## Caratteristiche

Python è un linguaggio fortemente e *dinamicamente tipizzato* (i tipi dati
esistono e sono necessari ma non è necessario dichiararli esplicitamente),
*case sensitive* (var e VAR sono due variabili diverse) e *object oriented*
(tutto in Python è un oggetto).

## Come ottenere aiuto

L'interprete di Python fornisce già un valido sistema di aiuto. Per
sapere come usare un oggetto basta digitare `help()`. Sono utili anche `dir`,
che elenca gli attributi (metodi) disponibili per l'oggetto,  e
`.__doc__` che mostra la documentazione completa quando disponibile:

    >>> help(5)
    Help on int object:
    (etc etc)

    >>> dir(5)
    ['__abs__', '__add__', ...]

    >>> abs.__doc__
    'abs(number) -> number\n\nReturn the absolute value of the
    argument.'

## Sintassi

In Python *non ci sono terminatori di riga obbligatori e i *blocchi sono
specificati con l' indentazione*. Indenta per cominciare un blocco e rimuovi
l'indentazione per concluderlo, tutto qui. Le istruzioni che richiedono un
blocco indentato terminano con i due punti (`:`). I *commenti* cominciano col
cancelletto (`#`) e sono a linea singola. Stringhe su più righe sono usate per
i *commenti multi linea*. Le *assegnazioni* si compiono col simbolo di
uguale (`=`). Per i *test di uguaglianza* si usa il doppo uguale (`==`).
Puoi aumentare e diminuire un valore usando gli operatori `+=` e `-=` seguiti
dall'addendo. Ciò funziona con molti tipi di dati, stringhe incluse. Puoi
assegnare e usare più variabili sulla stessa riga. Alcuni esempi:

    >>> myvar = 3
    >>> myvar += 2
    >>> myvar
    5

    >>> myvar -= 1
    >>> myvar
    4

    """Questo è un commento su più righe.
    Le righe seguenti vengono concatenate."""
    >>> mystring = "Hello"
    >>> mystring += " world."
    >>> print mystring
    Hello world.

    # Il codice seguente scambia due variabili in una sola riga.
    # Non ci sono errori di conversione di tipo perché
    # i nuovi valori non vengono assegnati. Vengono creati
    # nuovi oggetti ai quali le variabili fanno ora riferimento.
    >>> myvar, mystring = mystring, myvar

## Tipi di dati

Le strutture più significative in Python sono *liste, tuple e dizionari*. I Set
sono integrati in Python a partire dalla versione 2.5 (per le versioni
precedenti sono disponibili nella libreria `sets`). Le Liste sono simili ad
array mono dimensionali ma è possibile creare liste che contengono altre liste.
I dizionari sono array che contengono coppie di chiavi e valori (hash table)
e le tuple sono oggetti immutabili mono dimensionali. In Python gli array
possono essere di qualunque tipo, quindi puoi mischiare interi, stringhe, ecc
nelle tue liste/dizionari e tuple. L'indice del primo oggetto in qualunque tipo
di array è sempre zero. Gli indici negativi sono ammessi e contano a partire
dalla fine dell'array, -1 indica l'ultimo elemento dell'array. Le variabili
possono fare riferimento a funzioni.

    >>> esempio = [1, ["un'altra", "lista"], ("una", "tupla")]
    >>> mialista = ["Elemento 1", 2, 3.14]
    >>> mialista[0] = "Ancora elemento 1"
    >>> mialista[-1] = 3.15
    >>> miodizionario = {"Key 1": "Valore 1", 2: 3, "pi": 3.14}
    >>> miodizionario["pi"] = 3.15
    >>> miatupla = (1, 2, 3)
    >>> miafunzione = len
    >>> print miafunzione(mialista)
    3

Puoi ottenere un *range di array* usando i due punti (`:`). Non indicare
l'indice iniziale del range sottintende il primo elemento; non indicare
l'indice finale sottintende l'ultimo elemento. Indici negativi contano
a partire dall'ultimo elemento (-1 è l'ultimo elemento dell'array). Quindi:

    >>> mialista = ["Elemento 1", 2, 3.14]
    >>> print mialista[:]
    ['Elemento 1', 2, 3.1400000000000001]

    >>> print mialista[0:2]
    ['Elemento 1', 2]

    >>> print mialista[-3:-1]
    ['Elemento 1', 2]

    >>> print mialista[1:]
    [2, 3.14]

## Stringhe

Le stringhe in Python sono indicate *indifferentemente con la virgoletta
singola (`'`) o doppia (`"`) ed è consentito usare una notazione all'interno
di una stringa delimitata dall'altra (`"Egli disse 'ciao'."` è valida).
Stringhe su più righe sono racchiuse in triple (o singole) virgolette (`"""`).
Python *supporta Unicode, basta ricorrere alla sintassi `u"Questa è una stringa
unicode"`. Per *inserire valori in una stringa* usa l'operatore `%` (modulo)
e una tupla. Ogni % viene sostituito da un elemento della tupla, da sinistra
a destra, ed è consentito usare un dizionario per le sostituzioni.

    >>> "Nome: %s\nNumero: %s\nStringa: %s" % (miaclasse.nome, 3, 3 * "-")
    Nome: Poromenos
    Numero: 3
    Stringa: ---

    strString = """Questa è
    una stringa
    multi riga."""

    # ATTENZIONE: Nota la s finale in "%(key)s".
    >>> print "Questo %(verbo)s un %(nome)s." % {"nome": "test", "verbo": "è"}
    Questo è un test.

## Controllo di flusso

Le istruzioni per il controllo di flusso sono `if`, `for`, e `while`. Non esiste il `select`; al suo posto si usa `if`. Il `for` si usa anche per enumerare i membri di una lista. Per ottenere un elenco di numeri si usa `range(numero)`.

    rangelist = range(10)
    >>> print rangelist
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

    for number in rangelist:
        # Verifica se numer è uno dei
        # numeri nella tupla.
        if number in (3, 4, 7, 9):
            # "Break" termina un for senza
            # eseguire la clausola "else".
            break
        else:
            # "Continue" prosegue con l'iterazione successiva
            # del loop. Piuttosto inutile in questo caso,
            # visto che siamo all'ultima istruzione del loop.
            continue
    else:
        # Questo "else" è opzionale ed è
        # eseguito solo se il loop non è stato interrotto
        # con "break".
        pass # Non fa nulla

    if rangelist[1] == 2:
        print "Il secondo elemento (le liste sono 0-based) è 2"
    elif rangelist[1] == 3:
        print "Il secondo elemento (le liste sono 0-based) è 3"
    else:
        print "Non saprei"

    while rangelist[1] == 1:
        pass

## Funzioni

Le funzioni sono dichiarate con la la parola chiave `def`. Eventuali *argomenti
opzionali vanno dichiarati dopo quelli obbligatori e devono avere un valore
assegnato. Quando si chiamano funzioni passando *argomenti per nome
è necessario passare anche il valore. Le funzioni possono restituire una tuple
(lo spacchettamento delle tuple rende possibile la restituzione di *valori
multipli). Le *lambda sono funzioni in linea. I parametri sono passati *per
riferimento*, ma i tipi immutabili (tuple, interi, stringhe, ecc.) non possono
essere modificati nella funzione. Questo succede perché *viene passata solo la
posizione in memoria* dell'elemento, e assegnare un altro oggetto alla
variabile *comporta la perdita del riferimento* all'oggetto precedente. Per
esempio:

    # Equivalente a def f(x): return x + 1
    funzionevar = lambda x: x + 1
    >>> print funzionevar(1)
    2

    # un_int e una_stringa sono opzionali, hanno valori di default
    # da usare se non vengono passati (2 e "Una stringa", rispettivamente).
    def passing_example(una_lista, un_int=2, una_stringa="Una stringa"):
        una_lista.append("Nuovo elemento")
        un_int = 4
        return una_lista, un_int, una_string

    >>> mia_lista = [1, 2, 3]
    >>> mio_int = 10
    >>> print passing_example(mia_lista, mio_int)
    ([1, 2, 3, 'Nuovo elemento'], 4, "Una stringa")

    >>> mia_lista
    [1, 2, 3, 'Nuovo elemento']

    >>> mio_int
    10

## Classi

Python supporta la *ereditarietà multipla* delle classi. Le variabili
e i metodi privati vengono dichiarati per convezione (non è una regola del
linguaggio) precedendoli con due underscore (_). Possiamo assegnare *attributi
(proprietà) arbitrari* alle istanze di una classe. Un esempio:

    class MiaClasse:
        comune = 10
        def __init__(self):
            self.miavariabile = 3
        def miafunzione(self, arg1, arg2):
            return self.miavariabile

    # Creiamo una istanza della classe
    >>> istanza = MiaClasse()
    >>> istanza.miafunzione(1, 2)
    3

    # Questa variabile è condivisa da tutte le istanze
    >>> istanza2 = MiaClasse()
    >>> istanza.comune
    10

    >>> istanza2.comune
    10

    # Nota come qui usiamo il nome della classe
    # invece dell'istanza.
    >>> MiaClasse.common = 30
    >>> instanza.common
    30

    >>> instanza2.common
    30

    # Questo non aggiornerà la variabile nella classe,
    # invece assegnerà un nuovo oggetto alla variabile
    # della prima istanza.
    >>> istanza.common = 10
    >>> istanza.common
    10

    >>> istanza2.common
    30

    >>> MiaClasse.common = 50

    # Il valore non è cambiato perché "common"
    # ora è una variabile dell'istanza.
    >>> istanza.common
    10

    >>> istanza2.common
    50

    # Questa classe eredita da MiaClasse. L'ereditarietà
    # multipla viene dichiarata così:
    # class AltraClasse(MiaClasse1, MiaClasse2, MiaClasseN)
    class AltraClasse(MiaClasse):
        # L'argomento "self" è passato automaticamente
        # e fa riferimento all'istanza della classe, quindi puoi impostare
        # variabili di istanza come sopra, ma dall'interno della classe.
        def __init__(self, arg1):
            self.miavariabile = 3
            print arg1

    >>> istanza = AltraClasse("hello")
    hello

    >>> istanza.miafunzione(1, 2)
    3

    # Questa classe non ha un membro (proprietà) .test member, ma
    # possiamo aggiungerne uno all'istanza quando vogliamo. Nota
    # che .test sarà un membro della sola istanza.
    >>> istanza.test = 10
    >>> istanza.test
    10

## Eccezioni

Le eccezioni in Python sono gestite con dei blocchi `try-except [nome_eccezione]`:

    def una_funzione():
        try:
            # Divisione per zero causa una eccezione
            10 / 0
        except ZeroDivisionError:
            print "Oops, errore."
        else:
            # Non c'è stata eccezione, possiamo proseguire.
            pass
        finally:
            # Questo codice viene eseguito quando il blocco
            # try..except è già eseguito e tutte le eccezioni
            # sono state gestite, anche se si verifica una nuova
            # eccezione direttamente nel blocco.
            print "Abbiamo finito."

    >>> una_funzione()
    Oops, errore.
    Abbiamo finito.

## Importare librerie

Le librerie esterne si importano con `import [nomelibreria]`. Puoi anche usare la forma `[nomelibreria] import [nomefunzione]` per importare singole funzioni. Ecco un esempio:

    import random
    from time import clock

    randomint = random.randint(1, 100)

    >>> print randomint
    64

## Input e Output

Python vanta una vasta gamma di librerie per gestire input/output di files. In
questo esempio vediamo come *serializzare* (convertire strutture dati in
stringhe) usando la libreria `pickle`:

    import pickle
    mialista = ["Questo", "è", 4, 13327]

    # Apre il file C:\binary.dat in scrittura. La lettera r
    # prima del nome file serve a evitare l'escaping
    # del backslash.
    miofile = file(r"C:\binary.dat", "w")

    pickle.dump(mialista, miofile)
    miofile.close()

    miofile = file(r"C:\text.txt", "w")
    miofile.write("Questa è una stringa di prova")
    miofile.close()

    miofile = file(r"C:\text.txt")

    >>> print miofile.read()
    'Questa è una stringa di prova'

    miofile.close()

    # Apre il file in lettura.
    miofile = file(r"C:\binary.dat")
    listadafile = pickle.load(miofile)
    miofile.close()

    >>> print listadafile
    ['Questo', 'è', 4, 13327]

## Varie ed eventuali

I *test possono essere concatenati. `1 > a < 3` verifica che a sia minore di  3
e maggiore di 1. Puoi usare `del` per *cancellare variabili o elementi di
array*. Le *comprensioni di lista* sono uno strumento potente per creare
e manipolare le liste. Consistono in una espressione seguita da una clausola
`for` seguita da zero o più clausole `if`. Quindi: 

    >>> lst1 = [1, 2, 3]
    >>> lst2 = [3, 4, 5]
    >>> print [x * y for x in lst1 for y in lst2]
    [3, 4, 5, 6, 8, 10, 9, 12, 15]
    >>> print [x for x in lst1 if 4 > x > 1]
    [2, 3]

    # Verifica se almeno un elemento ha una determinata
    # caratteristica.
    # "any" restituisce true se qualunque elemento nella
    # lista è vero.
    >>> any([i % 3 for i in [3, 3, 4, 4, 3]])
    True
    # Funziona perché 4 % 3 = 1, e 1 in Python è true,
    # quindi any() restituisce True.

    # Verifica quanto elemento hanno una determinata
    # caratteristica.
    >>> sum(1 for i in [3, 3, 4, 4, 3] if i == 4)
    2

    >>> del lst1[0]
    >>> print lst1
    [2, 3]

    >>> del lst1

Le *variabili globali* vengono dichiarate all'esterno delle funzioni
senza dichiarazioni particolari, ma se desideri modificarle in una funzione
devi dichiararle con la parola `global` all'inizio della funzione,
altrimenti Python assegnerà quell'oggetto a una nuova variabile locale
(presta attenzione, si tratta di un piccolo dettaglio che può metterti
facilmente nei guai). Per esempio: numero = 5

    def miafunz():
        # Questo stamperà 5.
        print numero

    def altrafunz():
        # Questo solleva una eccezione perché la variabile
        # non è stata ancora assegnata. Python crea un
        # nuovo oggetto locale invece di accedere al globale
        print numero
        numero = 3

    def ancorafunz():
        global numero
        # Questo cambierà il valore alla variabile globale
        numero = 3

## Epilogo

Questa non intende essere una guida completa (e nemmeno parziale) a Python.
Python ha una vasta gamma di librerie e molte, moltissime funzionalità che
dovrai scoprire con altri mezzi, come [Dive Into Python][2] (tradotto in
italiano) o l'eccellente [Learning Python di Mark Lutz][4], libro che consiglio
a chiunque voglia davvero imparare e capire Python.

Mi auguro di averti aiutato nella transizione verso Python. Lasciami un
commento se pensi che ci sia qualcosa da migliorare o se c'é qualcos'altro
che vorresti approfondire.

Sono [@nicolaiarocci][3] su Twitter.

 [1]: http://www.korokithakis.net/tutorials/python
 [2]: http://it.diveintopython.net/
 [3]: http://twitter.com/nicolaiarocci
 [4]: http://www.amazon.it/gp/product/0596158068/ref=as_li_ss_tl?ie=UTF8&camp=3370&creative=24114&creativeASIN=0596158068&linkCode=as2&tag=nicoiaro-21
