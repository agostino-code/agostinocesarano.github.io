---
title: Sistemi Informativi Multimediali (Indicizzazione e Recupero)
date: 2022-06-03T13:49:12.572Z
author: Agostino Cesarano
summary: Appunti per il corso di SIM, Professore Balzano; seconda parte,
  Indicizzazione e Recupero dei Dati.
tags:
  - SIM
---
##### Indicizzazione e Recupero

**Differenze tra DBMS e IR**

**DBMS**

Struttura omogenea dei record, i componenti del record sono per lo più gli attributi.

Un record è definito completamente ed univocamente dai propri attributi.

> Retrieval con match esatto.

**IR**

* Records non strutturati
* Attributi non prefissati

Indicizzazione del documento, recupero di keywords.

> Retrieval con match approssimato o parziale.

**Processo base del Document Retrieval**

Il processo di Document Retrieval si divide in due fasi:

* Online
* Offline

![Retrieval dei Documenti](/static/img/retrieval.png "Retrieval dei Documenti")

**Retrieval Off-Line**

Riceve dei Documenti è li processa in modo da estrarre le caratteristiche fondamentali.

**Retrieval On-Line**

Riceve una Query, analizza quelle che sono le informazioni da ricercare.

Successivamente confronta le informazioni da cercare con le caratteristiche dei dati precedentemente processati nella parte Off-Line dell' processo di ricerca.

Una volta trovati i documenti che abbiano caratteristiche simili a quelli ricercate, vengono mostrate all'utente che può:

* Raffinare la sua ricerca.
* Fornire un feedback sui documenti visualizzati ( Caratteristica non sempre presente in tutti gli IR).