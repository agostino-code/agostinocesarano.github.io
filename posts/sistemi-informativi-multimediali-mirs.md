---
title: Sistemi Informativi Multimediali (MIRS)
date: 2022-05-24T08:21:00.876Z
author: Agostino Cesarano
summary: Appunti per il corso di SIM, Professore Balzano; seconda parte, i MIRS.
tags:
  - SIM
---
##### Architettura dei MIRS

![Architettura di un MIRS](/static/img/architettura-mirs.png "Architettura di un MIRS")

La prima fase è quella di inserimento nel MIRS.

**Fase 1 (Inserimento)**

1. L'Utente specifica un tipo di Input ( microfono, CD, videocamera ).
2. I contenuti vengono estratti dal database automaticamente o semi-automaticamente.
3. Gli oggetti vengono inviati al server, con le relative caratteristiche.
4. Gli oggetti in arrivo vengono organizzati e spediti al prossimo blocco.
5. Esegue l'indicizzazione delle informazione.
6. Memorizza le informazioni indicizzate e gli oggetti.

La seconda fase è quella del recupero delle informazione, il modello è lo stesso cambia il tipo di operazioni effettuate.

**Fase 2 (Recupero)**

1. L'Utente esegue una Query sul database, l'oggetto ricercato può anche non essere presente.
2. Vengono analizzata la Query.
3. Il Client raccoglie i dati che la query richiede.
4. Il Server riceve i dati e li smista alla indicizzazione.
5. Il motore di indicizzazione reperisce gli elementi nel database più pertinenti alla ricerca.
6. Recupero dell'oggetto richiesto ed invio all'interfaccia utente.

**Modello dei Dati**

Un DBMS ha la finalità di archiviare i dati, tenendo conto di *tipo e proprietà dell'oggetto* che dovrà contenere.

Il modello dei dati di un MIRS deve soddisfare alcuni requisiti:

* Estensibilità a nuovi tipi di dati.
* Flessibilità, deve permettere inserimento e ricerca.
* Predisposizione, per la rappresentazione di dati semplici e complessi.
* Efficienza nelle strategie di memorizzazione e ricerca.
* Incapsulamento di codice e dati in una singola unità, singolo oggetto.

Il codice definisce le operazioni effettuabili sui dati.

Il modello dei dati si divide in tre parti principi chiamate Layer:

* Layer Oggetto
* Layer Tipo
* Layer Formato

> Il Layer Oggetto è costituito da relazioni:
>
> 1. Spaziale
> 2. Temporale
> 3. Composito

Che specificano ciò che sono i dettagli dell'oggetto.

Sincronizzazione audio - video o immagini, testo, posizione di apparizione.

> Il Layer Tipo è costituito dai tipi principali di media:
>
> 1. Testo
> 2. Immagine
> 3. Grafica
> 4. Audio
> 5. Video

Queste informazioni vengono usate nella fase di ricerca, ogni tipo ha un suo dato significativo.

Testo ( numeri caratteri testuali )

Immagine ( dimensione in pixel, istogramma di colore, oggetti contenuti nell'immagine )

Grafica ( elementi che compongono la scena )

Audio ( durata audio )

Video ( durata video, keyframes )

> Il Layer Formato specifica il formato con cui il media è memorizzato.

**Modello di un video**