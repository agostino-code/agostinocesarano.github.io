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
> un processore pu`o risolvere un problema.
>
> **Processore:** e la macchina che eseguirà il processo descritto dal
> programma; non si deve intendere come un singolo oggetto, ma
> come una architettura di elaborazione.
>
> **Programma:** è l’espressione codificata di un processo.

**Come vedere se un linguaggio è Completo?**

I linguaggi di progammazione *computazionalmente completi*, sono quelli che possono
programmare qualunque funzione calcolabile.

1. Un linguaggio di progammazione è completo se può simulare una macchina di Turing.
2. Sono completi solo quelli che riescono ad esprimere anche programmi di cui non è decidibile la terminazione.

**Macchine Astratte**

Una macchina astratta per un linguaggio di Progammazione è un insieme di strutture di dati e algoritmi che permettono di memorizzare progammi scritti in quel linguaggio.

> Quando traduciamo il linguaggio di progammazione non lo traduciamo su una **macchina hardware** ma su una macchina di livello superiore.

Ad esempio Java utilizza una macchina astratta JVM che traduce tramite Software il codice da tradurre.

*Compilazione per macchina intermedia.*

> **Interpreti:** traducono ed eseguono un costrutto alla volta.

**PRO**: debug - fase di sviluppo: interazione piu snella.

> Compilatori: prima traducono l’intero programma; poi la
> traduzione puo essere eseguita (anche piu volte).

**PRO**: velocita di esecuzione finale - fase di rilascio.

**PRO**: più controlli e in anticipo

Interpetre nella compilazione per macchina intermedia è detta **Supporto Run Time (SRT)**

*L'SRT* ha funzionalità aggiuntive

*Funzioni di basso livello / interfacce col S.O. ;* 

ad es. funzionidi I/O.

*Gestione della memoria;* 

garbage collection; gestione dell’heap; gestione dello stack.

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

meno eccezzioni alle regole del linguaggio.

> Portabilità

**Criterio di scelta del linguaggio**

* Disponibilita dei traduttori
* Maggiore conoscenza da parte del programmatore
* Esistenza di standard di portabilita
* Comodita dell’ambiente di programmazione
* Sintassi aderente al problema
* Semantica aderente alla architettura fisica?
  *con le moderne tecniche di implementazione dei linguaggi non è più un criterio stringente*

**Paradigmi computazionali**

> **Imperativo:** Un programma specifica sequenze di modifiche da apportare allo stato della macchina (memoria).
>
> *Progammi di tipo ( iterativo )*
> **Funzionale:** Il programma e le sue componenti sono funzioni. Esecuzione come valutazione di funzioni.
>
> *Progammi di tipo ( ricorsivo )*
> **Logico:** Programma come descrizione logica di un problema. Esecuzione analoga a processi di dimostrazione di teoremi.
> **Orientato ad oggetti:** Programma costituito da oggetti che scambiano messaggi.
> **Parallelo:** Programmi che descrivono entit`a distribuite che sono eseguite contemporaneamente ed in modo asincrono.

*I linguaggi di progammazione modermi permettono di usare più paradigmi in base alle nostre esigenze.*

*Esempio:*

*Vogliamo scrivere in un linguaggio imperativo, funzionale e logico la funzione* **membro(X,L)** *che decida se l’elemento X appartiene alla lista L.*

*Useremo tre funzioni* 

* empty() restituisce **true** se la lista è vuota.
* testa() restituisce il valore di testa.
* coda() restituisce la coda tagliando il valore di testa.

*In pseduo codice, paradigma imperativo.*

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

*In Lisp ( paradigma funzionale )*

```lisp
function member (X,L)
if vuota (L) then false
else if X == testa (L) then true
else member (X, coda (L))
```