---
title: Linguaggi di Progammazione
date: 2022-03-10T23:13:22.891Z
author: Agostino Cesarano
summary: Appunti per il corso di Linguaggi di Progammazione, Professore Bonatti.
tags:
  - LP
---
**Terminologia**

> **Linguaggio di programmazione:** è un linguaggio che è usato
> per esprimere (mediante un programma) un processo con il quale
> un processore può risolvere un problema.
>
> **Processore:** e la macchina che eseguirà il processo descritto dal
> programma; non si deve intendere come un singolo oggetto, ma
> come una architettura di elaborazione.
>
> **Programma:** è l’espressione codificata di un processo.

**Come vedere se un linguaggio è Completo?**

I linguaggi di programmazione *computazionalmente completi*, sono quelli che possono
programmare qualunque funzione calcolabile.

1. Un linguaggio di programmazione è completo se può simulare una macchina di Turing.
2. Sono completi solo quelli che riescono ad esprimere anche programmi di cui non è decidibile la terminazione.

**Macchine Astratte**

Una macchina astratta per un linguaggio di Programmazione è un insieme di strutture di dati e algoritmi che permettono di memorizzare programmi scritti in quel linguaggio.

> Quando traduciamo il linguaggio di programmazione non lo traduciamo su una **macchina hardware** ma su una macchina di livello superiore.

Ad esempio Java utilizza una macchina astratta JVM che traduce tramite Software il codice da tradurre.

*Compilazione per macchina intermedia.*

> **Interpreti:** traducono ed eseguono un costrutto alla volta.

**PRO**: debug - fase di sviluppo: interazione più snella.

> Compilatori: prima traducono l’intero programma; poi la
> traduzione può essere eseguita (anche più volte).

**PRO**: velocita di esecuzione finale - fase di rilascio.

**PRO**: più controlli e in anticipo

Interprete nella compilazione per macchina intermedia è detta **Supporto Run Time (SRT)**

*L'SRT* ha funzionalità aggiuntive

*Funzioni di basso livello / interfacce col S.O. ;* 

ad es. funzioni di I/O.

*Gestione della memoria;* 

garbage collector; gestione dell’heap; gestione dello stack.

##### Proprietà dei linguaggi

> Semplicità

*( concisione ) vs ( leggibilità )*

*Semantica:* minimo numero di concetti e strutture.

*Sintattica:* unica rappresentazione di ogni concetto.

> Astrazione

*Dati:* nasconde i dettagli dei vari oggetti.

*Procedure:* facilitare la modularità del progetto.

> Espressività

*( facilità di rappresentazione di oggetti ) vs (semplicità)*

> Ortoganità

meno eccezioni alle regole del linguaggio.

> Portabilità

**Criterio di scelta del linguaggio**

* Disponibilità dei traduttori
* Maggiore conoscenza da parte del programmatore
* Esistenza di standard di portabilità
* Comodità dell’ambiente di programmazione
* Sintassi aderente al problema
* Semantica aderente alla architettura fisica?
  *con le moderne tecniche di implementazione dei linguaggi non è più un criterio stringente*

**Paradigmi computazionali**

> **Imperativo:** Un programma specifica sequenze di modifiche da apportare allo stato della macchina (memoria).
>
> *Programmi di tipo ( iterativo )*
> **Funzionale:** Il programma e le sue componenti sono funzioni. Esecuzione come valutazione di funzioni.
>
> *Programmi di tipo ( ricorsivo )*
> **Logico:** Programma come descrizione logica di un problema. Esecuzione analoga a processi di dimostrazione di teoremi.
> **Orientato ad oggetti:** Programma costituito da oggetti che scambiano messaggi.
> **Parallelo:** Programmi che descrivono entità distribuite che sono eseguite contemporaneamente ed in modo asincrono.

*I linguaggi di programmazione moderni permettono di usare più paradigmi in base alle nostre esigenze.*

*Esempio:*

*Vogliamo scrivere in un linguaggio imperativo, funzionale e logico la funzione* **membro(X,L)** *che decida se l’elemento X appartiene alla lista L.*

*Useremo tre funzioni* 

* empty() restituisce **true** se la lista è vuota.
* testa() restituisce il valore di testa.
* coda() restituisce la coda tagliando il valore di testa.

*In pseudo codice, paradigma imperativo.*

```
procedure membro (X,L)
local L1 = L
while not vuota (L1) and not X= testa (L1)
do L1 = coda (L1)
return not vuota (L1)
```

*In C ( linguaggio di tipo imperativo )*

```c
bool member (X,L) {
List L1 = L;
while ( ! empty (L1) && ! X= testa (L1 ))
L1 = coda (L1 );
return (! empty (L1 ));
}
```

*pseudo codice ( paradigma funzionale )*

```lisp
function member (X,L)
if vuota (L) then false
else if X == testa (L) then true
else member (X, coda (L))
```

*In LISP ( linguaggio di tipo funzionale )*

```lisp
( defun membro (x l)
( cond (( null l) nil )
(( equal x ( first l)) T)
(T ( membro x ( rest l )))))
```

*C si potrebbe usare in stile funzionale se evitassimo di usare i costrutti imperativi:*

```ags
bool member (X,L) {
return ( vuota (L)) ? false :
(X == testa (L ))? true :
member (X, coda (L)) }
```

*In Prolog ( linguaggio di tipo Logico, paradigma logico )*

```
membro (X, [X|L]).
membro (X, [Y|L]) :- membro (X, L).
```

##### Memoria

*Consiste in un insieme di “contenitori di dati”.*

Ad es. parole (o celle) della memoria centrale.

Tipicamente rappresentate dal loro indirizzo associati ai valori in essi contenuti, i valori delle variabili.

Dunque (concettualmente) la memoria è:

* Una funzione da uno spazio di locazioni ad uno spazio di valori
* mem(loc) = “valore contenuto in loc”

> **mem(loc)** *\= locazione di memoria  --> valore*

**Assegnazioni**

Definizione grammaticale (sintassi):

```pascal
<name > <assignment - operator > <expression >

//Esempio in Pascal:
a := b + c;
```

*<name>* rappresenta la locazione dove viene posto il risultato.
*<expression>*sono specificati una computazione (espressione matematica) e i riferimenti ai valori necessari alla computazione.

**Modello Imperativo**

I programmi sono descrizioni di sequenze di modifiche della “memoria” del calcolatore.

Ogni unità di esecuzione consiste di 4 passi:

1. ottenere indirizzi delle locazioni di operandi e risultato;
2. ottenere dati di operandi da locazioni di operandi;
3. valutare risultato;
4. memorizzare risultato in locazione risultato.

In sostanza un assegnamento!

Il modello imperativo usa dei nomi come astrazione di indirizzi di locazioni di memoria **(variabili)**.

Quindi l'ambiente di esecuzione *(environment)* comprende:

Un insieme di nomi di variabili e parametri, non indirizzi di memoria ma identificatori.

Quindi l'ambiente di esecuzione associato ad un modello imperativo è una funzione, identificata come **env(id)** che dato un certo identificatore, per lo più variabili, ci restituisce la locazione di memoria identificata con quel nome.

> **env(id)** = identificatore --> locazione

A sua volta le funzioni *env* sono associate a funzioni *mem* che restituiscono i valori delle locazioni.

Il **valore di una variabile x è**:

>  mem( env ( x ))

Nel **paradigma funzionale**, non esiste la funzione *mem* e la funzione *env* associa direttamente gli identificatori al contenuto della memoria.

Nel paradigma imperativo la funzione *env* identifica una associazione immutabile (la locazione di memoria associata a un nome non cambia);

*Esempi di esercizi, può uscire all'esame!*

**\*(x+1)**=... **\-->** mem( env( x )) + 1

A destra si aggiunge un **mem** davanti.

...=**\*(x+1)** **\-->** **mem**( mem( env( x ) + 1)

...=**\*(x+y) --> mem**( mem( env(x) ) + mem( env(y) ))

> **Sempre SBAGLIATI!**
>
> env ( mem (...) )
>
> env ( x +1 )

**v\[ i ]** vettore di dimensione i = **\*(v+i) -->** mem( env(v) + mem( env(i))

**p\[ i ]** puntatore di dimensione i = **\*(p+i) -->** mem( mem( env(p) + mem( env(i))

Il puntatore è gestito come una locazione di memoria mentre il vettore no.

Quando c'è una & si toglie un mem, ad esempio.

v\[ 3 ] = &v\[ 3 ] **\-->** env( v ) + 3 = env ( v ) +3

**NO** v\[ 3 ] **\-->** **mem(** env ( v ) +3 **)**

**NO** &v\[ 3 ] **\--> mem(** env ( v ) +3 **) oppure env(mem(env**... **GRAVE! mai fare.**

Perché il vettore non viene visto come una variabile?

es. v\[ 3 ] = 1 indica dove scrivere "1" quindi quello che mi interessa è il solo indirizzo di quella casella del vettore.

p\[ 3 ] = &p\[ 3 ] **\-->** mem( env (p) +3 ) = mem( env ( p ) + 3 )

**NO mem(**mem( env ( p ) + 3 )**)**

&x = ... non c'è un mem da togliere **ERRORE non è un  l-value**

> **l-value** oggetto che occupa una posizione identificabile in memoria ( cioè ha un indirizzo ).
>
> **r-value** sono i restanti oggetti che non hanno un indirizzo.

##### Legame di tipo

Per definizione è correlato al legame di valore (ad es. il tipo di una variabile e il tipo del suo valore devono corrispondere).

Ogni volta che il legame di valore viene modificato, occorrerebbe controllare (**type checking**) la consistenza con il legame di tipo.

> Un linguaggio si dice **dinamicamente tipizzato** se il controllo del legame di tipo e di conseguenza anche il controllo di consistenza avviene durante l’esecuzione.

*Esempio: nei linguaggi di scripting e Python*

```python
x = 1; 
...
x= " abc ";
```

Inizialmente il tipo di x è un numerico, successivamente diventa un tipo stringa.

1. Gli identificativi non vengono dichiarati.
2. Gli assegnamenti determinano il tipo dell'identificatore.

Il tipo della variabile dipende dal valore che gli assegniamo, *avviene un type checking al cambio di valore.*

> Un linguaggio è **staticamente tipizzato** se il legame avviene durante la compilazione; in questo caso il controllo di consistenza può avvenire in entrambe le fasi.

##### Type checking

È il meccanismo di controllo di consistenza della coppia dei legami valore-tipo.

*Può avvenire:* 

1. durante la compilazione
2. durante l’esecuzione
3. per nulla

> Un linguaggio è **fortemente tipizzato** se il controllo di consistenza avviene sempre.

*Esempio di linguaggi fortemente tipizzati*

* Java è fortemente tipizzato.
* Pascal è quasi fortemente tipizzato (una sola eccezione di assenza di controllo: i record con varianti).

> Un linguaggio e **debolmente tipizzato** se il controllo di consistenza può non avvenire affatto in numerosi casi.

*Esempio di linguaggi debolmente tipizzati*

* C è debolmente tipizzato:
  in esso esistono le operazioni di casting, che consentono di forzare, in esecuzione, l’interpretazione di un qualunque valore secondo un qualunque tipo (anche un tipo diverso da quello a cui il valore è stato precedentemente associato);
  esistono puntatori a void, che godono, in esecuzione, di conversione di tipo implicita verso qualunque altro tipo puntatore;
  esistono le unioni, che sovrappongono la locazione di variabili di tipo diverso, senza controllare se il valore corrisponde al tipo con cui viene usato.

I linguaggi staticamente e fortemente tipizzati sono i più “forti” tra i fortemente tipizzati.

Quindi la strategia per i linguaggi **fortemente e staticamente tipati** è fare quanti più controlli possibile a tempo di compilazione ed eseguire i rimanenti a tempo di esecuzione perché prima si scoprono gli errori e più il testing diventa economico.

##### Blocchi di istruzioni

Le istruzioni nei linguaggi di programmazione moderni sono definiti in blocchi, questo è necessario per distinguere le varie componenti del codice ed assegnargli un nome.

Definiamo un piccolo pseudo-linguaggio per rappresentare un blocco:

```
...
BLOCK A;
  DECLARE I;
BEGIN A
  ... {I DEL BLOCCO A}
END A;
...
```

**Scoping**

In ambito **statico o lessicale.**

Blocchi annidati *vedono e usano i legami dei blocchi più esterni* (legami non locali) e, di solito, possono aggiungere legami locali o sovrapporne di nuovi.


In ambito **dinamico.**

Concetto qui esaminato solo in relazione ai blocchi annidati, ma che assume il proprio senso maggiore quando vi sono procedure chiamanti e chiamate. In questo caso *la procedura* *chiamata vede e usa i legami visti e usati dalla procedura chiamante.*

*Esempio Scoping Statico*

```
PROGRAM P;
  DECLARE X;
BEGIN P
... {X da P}
  BLOCK A;
    DECLARE Y;
  BEGIN A
    ... {X da P, Y da A}
    BLOCK B;
      DECLARE Z;
    BEGIN B
      ... {X da P, Y da A, Z da B}
    END B;
      ... {X da P, Y da A}
  END A;
    ... {X da P}
     BLOCK C;
       DECLARE Z;
     BEGIN C
        ... {X da P, Z da C}
     END C;
... {X da P}
END P;
```

Ogni blocco vede le variabili dichiarate dai blocchi più esterni è nel caso in cui è dichiarata una variabile locale con lo stesso identificativo, la variabile globale sarà sovrapposta con quella locale.