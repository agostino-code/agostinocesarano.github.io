---
title: Sistemi Informativi Multimediali
date: 2022-03-18T14:57:21.807Z
author: Agostino Cesarano
summary: Appunti per il corso di SIM, Professore Balzano.
tags:
  - SIM
---
##### Digitalizzazione

Con l'avvento dell'era digitale, è sempre stata maggiore l'esigenza di digitalizzare i dati, i dati che prima erano memorizzati su supporti fisici, cassette a nastro ecc.  con l' avvento della digitalizzazione sono memorizzati su file digitali; **media**.

Di conseguenza si è posto il problema su come gestire questi dati.

**Managment dei Dati**

I primi sistemi che permettono la gestione dei dati sono i Database.

I primi sono i DBMS *( Database Managment System )* che però potevano immagazzinare solo caratteri *AlfaNumerici* cioè dati testuali o numerici.

Successivamente con l'avvento dei MMDBMS *( MultiMedia DBMS )* è stata possibile l'immaganizzazione e la gestione dei media.

**RDBMS**

Gli RDBMS *(Relational DBMS)* costituiscono la tipologia maggiormente diffusa di DBMS ed hanno una struttura tabulare (Righe x Colonne):

**Righe ->** Elementi di informazione o RECORD.

**Colonne ->** Attributi o CAMPI.

L’ **SQL** *(Structured Query Language)* è utilizzato per la creazione delle tabelle, per l’inserimento ed il reperimento degli elementi dal DataBase.

I RDBMS permettono la memorizzazione di BLOB.

Il **BLOB** *(Binary Large Objects)* è una stringa binaria di lunghezza variabile che si utilizza per la memorizzazione di dati in formato binario come immagini.
**Nota:** sul BLOB non è possibile formulare un pattern di ricerca.

**OODBMS**

OODBMS *(Object‐Oriented DBMS)* è un tipo di DBMS orientato ad Oggetti, esso combina le capacità dei DataBase con le note proprietà degli Object Oriented (incapsulamento, eredità,…)

**Nota:** La differenza sostanziale tra un BLOB ed un *“oggetto”* è che l’ *“oggetto”* è propriamente definito e consente pertanto operazioni sulle sue proprietà (il BLOB invece no).

**IR (Information Retrieval)**

Costituiscono una parte rilevante tra i sistemi di recupero delle informazioni,essi operano prevalentemente in modalità testuale, ma possono essere ugualmente impiegati in ambito multimediale.

Mediante il testo è possibile fornire una descrizione *(Annotazione)* ai vari media *(Audio, Immagini, Video)* per permetterne, così, le successive consultazioni.

**Limiti degli IR:**

* L’Annotazione è per la gran parte manuale (e quindi dispendiosa in tempo);
* L’Annotazione è incompleta e soggettiva;
* Le query sono esclusivamente testuali;
* Molti oggetti sono difficili da descrivere (Textures, Oggetti di forme varie,…).

**MIRS (Multimedia Indexing and Retrieval Systems)**

Elaborazione estrazione delle caratteristiche