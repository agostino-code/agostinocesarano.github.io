---
title: Linguaggi di Progammazione
date: 2022-03-10T23:13:22.891Z
author: Agostino Cesarano
summary: Appunti per il corso di Linguaggi di Progammazione, Professore Bonatti.
tags:
  - LP
---
**Come vedere se un linguaggio è Completo?**

Un linguaggio di progammazione è completo se può simulare una macchina di Turing.

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