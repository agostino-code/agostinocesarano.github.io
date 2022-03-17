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

> Interpreti: traducono ed eseguono un costrutto alla volta.

**PRO**: debug - fase di sviluppo: interazione piu snella.

> Compilatori: prima traducono l’intero programma; poi la
> traduzione puo essere eseguita (anche piu volte).

**PRO**: velocita di esecuzione finale - fase di rilascio.

**PRO**: più controlli e in anticipo

Interpetre nella compilazione per macchina intermedia è detta **Supporto Run Time (SRT)**

L'SRT ha funzionalità aggiuntive

*Funzioni di basso livello / interfacce col S.O. ;* 

ad es. funzionidi I/O.

*Gestione della memoria;* 

garbage collection; gestione dell’heap; gestione dello stack.