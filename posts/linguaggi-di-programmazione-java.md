---
title: Linguaggi di Programmazione (Java)
date: 2022-03-31T08:44:49.217Z
author: Agostino Cesarano
summary: Appunti per il corso di LP, Professore Bonatti; seconda parte,
  approfondimenti su Java.
tags:
  - LP
---
##### Introduzione a Java

Con sintassi simile a C++ e semantica simile a SmallTalk.

È di solito menzionato (ma non serve solo) per produrre applet: applicazioni WEB che risiedono sul server ma sono eseguite dal browser WEB del cliente.

Le applicazioni Java sono programmi autonomi che non richiedono un browser WEB per essere eseguiti.

Tali programmi richiedono solo un elaboratore su cui sia installato Java Runtime Environment (**JRE**).

Il JRE può essere associato ad un **ambiente di sviluppo**, cioè un insieme di numerosi strumenti per la realizzazione di
programmi: un compilatore, un interprete, un generatore di documentazione, uno strumento di
aggregazione di file, . . .

I principali ambienti di sviluppo sono Intellij, Eclipse ecc.

In questo corso, compileremo i programmi nativamente senza l'utilizzo di **ambienti di sviluppo**.

```java
javac $nomefile.java //Comando per compilazione

java $nomefile.java //Comando per l'esecuzione
```

La compilazione crea dei file .class che contengono **bytecode** java, che successivamente vengono eseguiti dalla JVM installata su un qualsiasi dispositivo.

##### JVM (Java Virtual Machine)

La Java Virtual Machine è una macchina virtuale che è emulata dalla macchina reale.

I programmi per la JVM sono contenuti in file .class, ciascuno dei quali contiene al più una classe pubblica.

**Punti di vista**

Dal punto di vista della realizzazione, la JVM specifica:

* l’insieme di istruzioni della CPU;
* l’insieme dei registri;
* il formato del file Class;
* lo stack di esecuzione;
* lo heap gestito dal **garbage collector**;
* l’area di memoria.

Dal punto di vista dell’utilizzatore:

* Il formato del programma compilato, eseguibile dalla JVM, consiste in bytecode molto compatti ed efficienti.
* La maggior parte del type-checking è svolto durante la compilazione.
* Ogni realizzazione della JVM deve essere capace di eseguire un qualunque programma conforme alle specifiche della JVM.

**Garbage Collector**

La memoria allocata che non e più necessaria deve essere resa disponibile.

In altri linguaggi la de-allocazione e responsabilità del programmatore.

Java fornisce un thread a livello di sistema per tracciare l’allocazione di memoria.

Il Garbage Collector:

* ricerca e libera la memoria non più necessaria;
* è eseguito automaticamente;
* è dipendente dalle varie realizzazioni di JVM.