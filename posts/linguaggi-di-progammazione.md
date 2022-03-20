---
title: Linguaggi di Progammazione
date: 2022-03-10T23:13:22.891Z
author: Agostino Cesarano
summary: Appunti per il corso di Linguaggi di Progammazione, Professore Bonatti.
tags:
  - LP
---
**ù**

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