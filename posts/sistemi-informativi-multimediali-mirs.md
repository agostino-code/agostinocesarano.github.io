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

Il modello generale di un video è un:

Episodio -> Scene -> Shot -> Frame

Un Episodio si divide in più Scene e ogni scena si divide in più Shot, gli shot a loto volta in più Frame.

Ad ogni livello di dati vengono assegnati gli attributi relativi:

Episodio: autore, data di creazione, tipo di video, produttore, ecc…

Scena: attributi comuni agli Shot che contiene.

Shot (ripresa): frame chiave, oggetto ripreso, data, luogo.

Frame: statistiche sull’immagine, distribuzione del colore, ecc…

##### Interfaccia utente

Requisiti principali di una interfaccia utente di un MIRS:

1. Deve fornire gli strumenti per inserire oggetti nel database.
2. Deve fornire strumenti per definire efficacemente le query e le esigenze di ricerca dell'utente.
3. Presentare i risultati delle ricerche in maniera efficace.
4. Essere user-friendly, facile da usare.

**Popolazione del Database**

A differenza dei DBMS tradizionali in un MIRS i dati sono costituiti da media diversi e non hanno struttura ed attributi prefissati.

**Fase di Ricerca**

Le query che possono essere inviate ad un MIRS sono:

* Multiformi l’utente può ricercare l'elemento in modi differenti e tipi di media differenti;
* Incerte: l’utente sa cosa vuole ma non sa descriverlo e riconosce il risultato corretto solo quando lo vede.

**Raffinamento delle Query**

Spesso per query “incerte” occorre una fase di browsing: l’utente sa riconoscere quello che cerca ma non sa bene come descriverlo:

* richiesta vaga e presentazione di un insieme ampio di risultati
* ricerca su una tassonomia che organizza le informazioni (categorie, ecc…)
*  ricerca casuale su un insieme di risultati forniti a caso

Data l’incertezza delle query sui dati multimediali, l’utente deve poter raffinare le sue richieste in base ai risultati ottenuti per la richiesta iniziale.

> Se l’utente si vede restituito dal sistema un elemento abbastanza simile a quello cercato, il sistema deve permettergli di riutilizzarlo per effettuare una nuova ricerca, più raffinata.

Tale processo può essere ripetuto più volte.

La conoscenza del dominio e il profilo utente possono essere utilizzati per raffinare una query.

Un feedback sulla pertinenza è particolarmente utile nelle applicazioni multimediali.

> Nella pratica, il processo di individuazione di un’informazione multimediale è una combinazione delle fasi di ricerca, browsing e raffinamento.

**Estrazione delle caratteristiche/feature**

Gli oggetti multimediali gestiti dal database sono preprocessati per estrarne caratteristiche ed attributi.

I requisiti per l’estrazione delle feature sono:

* Le feature estratte devono essere complete e rappresentare il contenuto e l’informazione presente nel dato.
* Devono essere memorizzate in maniera compatta è facili da caricare ( altrimenti sarebbe più efficace rifare la ricerca ).

**Tipi di feature**

**METADATATI**

Catturano le informazioni di contesto che non descrivono o interpretano il contenuto del dato stesso (autore, data di creazione, titolo, ecc…)

**ANNOTAZIONI TESTUALI**

Sono descrizioni testuali del contenuto di un dato multimediale (possono essere soggettive e incomplete)

**FEATURE DI BASSO LIVELLO**

In genere possono essere estratte automaticamente

Catturano dati e statistiche di un oggetto e le relazioni spazio temporali tra parti dell’ oggetto

* Audio: volume medio, distribuzione in frequenza
* Immagini: distribuzione del colore, tessitura, forma degli oggetti,…
* Video: struttura temporale e feature dei singoli frame

**FEATURE DI ALTO LIVELLO**

In genere l’estrazione richiede l’intervento umano.

Cercano di riconoscere e capire gli oggetti: per esempio se in un file audio c’è musica o parlato.

Quindi operazioni più complesse è difficilmente eseguibili da una macchina.