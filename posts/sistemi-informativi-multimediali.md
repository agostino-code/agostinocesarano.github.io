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

##### Managment dei Dati

I primi sistemi che permettono la gestione dei dati sono i Database.

I primi sono i DBMS *( Database Managment System )* che però potevano immagazzinare solo caratteri *Alfanumerici* cioè dati testuali o numerici.

Successivamente con l'avvento dei MMDBMS *( MultiMedia DBMS )* è stata possibile l'immaganizzazione e la gestione dei media.

##### RDBMS

Gli RDBMS *(Relational DBMS)* costituiscono la tipologia maggiormente diffusa di DBMS ed hanno una struttura tabulare (Righe x Colonne):

**Righe ->** Elementi di informazione o RECORD.

**Colonne ->** Attributi o CAMPI.

L’ **SQL** *(Structured Query Language)* è utilizzato per la creazione delle tabelle, per l’inserimento ed il reperimento degli elementi dal Database.

I RDBMS permettono la memorizzazione di BLOB.

Il **BLOB** *(Binary Large Objects)* è una stringa binaria di lunghezza variabile che si utilizza per la memorizzazione di dati in formato binario come immagini.
**Nota:** sul BLOB non è possibile formulare un pattern di ricerca.

##### OODBMS

OODBMS *(Object‐Oriented DBMS)* è un tipo di DBMS orientato ad Oggetti, esso combina le capacità dei DataBase con le note proprietà degli Object Oriented (incapsulamento, eredità,…)

**Nota:** La differenza sostanziale tra un BLOB ed un *“oggetto”* è che l’ *“oggetto”* è propriamente definito e consente pertanto operazioni sulle sue proprietà (il BLOB invece no).

##### IR (Information Retrieval)

Costituiscono una parte rilevante tra i sistemi di recupero delle informazioni, essi operano prevalentemente in modalità testuale, ma possono essere ugualmente impiegati in ambito multimediale.

Mediante il testo è possibile fornire una descrizione *(Annotazione)* ai vari media *(Audio, Immagini, Video)* per permetterne, così, le successive consultazioni.

##### Limiti degli IR:

* L’Annotazione è per la gran parte manuale (e quindi dispendiosa in tempo);
* L’Annotazione è incompleta e soggettiva;
* Le query sono esclusivamente testuali;
* Molti oggetti sono difficili da descrivere (Textures, Oggetti di forme varie,…).

#### MIRS (Multimedia Indexing and Retrieval Systems)

Il MIRS è il sistema di gestione dei media basato su:

1. Elaborazione e estrazione delle caratteristiche
2. Preelaborazione e indicizzazione

Questo sistema permette di fare ricerche dettagliate sulle varie componenti del media ( Query), il sistema pre mastica i dati è ne individua le pecularità.

![Schema di funzionamento MIRS](/static/img/mirs-scheme.png "MIRS schema di funzionamento")

Quindi il sistema effettua un **Indexing -> Indicizzazione** e in base ai parametri di ricerca effettua un **Retrival -> Recupero** dei dati che rispettano le nostre richieste.

Questo sistema è usato dai moderni motori di ricerca, es. Google.

##### Proprietà

Alcune delle proprietà attese in un MIRS sono:

Query su **METADATI**

es. nome_autore, data_creazione,…

Query su **ANNOTAZIONI**

es. Con riferimento al testo descrittivo (inserito manualmente) relativo all’oggetto considerato

Query su **MODELLI di DATI o CARATTERISTICHE**

es. Con riferimento ad una caratteristica come la distribuzione del colore, …

Query su **ESEMPI**

es. ricercare un oggetto multimediale, specificando un oggetto similare (come un’immagine, un suono, un disegno.

Query su **APPLICAZIONI SPECIFICHE**

es. ricercare qualcosa mediante informazione molto specifiche e dettagliate, come la grandezza di un oggetto oppure l’età di una persona.

##### Applicazioni

Medicina

es. Confronto dell’ecografia di un paziente con tutto il D.B. delle ecografie

**Sicurezza**

es. Riscontro della foto di una persona con un D.B. di ricercati

**Didattica**

es. ricercare il nome di un animale di cui si possiede solo una foto e/o registrazione del suo verso

**Editoria**

es. ricercare una persona di cui non si conosce il nome ma l’immagine, tra i giornali, foto e filmati degli ultimi 20 anni

**Intrattenimento**

es. cercare in un vasto D.B. un video divertente come quello appena visto

**Copyright**

es. cercare in un D.B. di brevetti eventuali oggetti simili a quello che dovrebbe essere brevettato.

##### Tipologia e Formati dei Dati Multimediali

L'obiettivo principale di un MIRS è quello di **Indicizzare e Ricercare i dati Multimediali** tra cui testi, grafica, immagini, audio, video.

Un MIRS è quindi molto diverso da un DBMS; per la progettazione di un MIRS è pertanto necessario conoscere
la struttura, le caratteristiche e le peculiarità dei dati multimediali. 

**In particolare:**

* In che modo vengono memorizzati i dati;
* Le tecniche standard di compressione;
* Modalità e complessità del processo di estrazione ed indicizzazione delle caratteristiche
* Requisiti di memorizzazione;
* Requisiti di comunicazione;
* Requisiti per la presentazione.

##### Il Testo

La gran parte delle informazioni sono codificate con testo di caratteri alfanumerici e sono tradizionalmente rappresentati mediante il codice *ASCII.*

I caratteri vengono rappresentati mediante 8 bit e i caratteri stampabili vanno dal 32 al 126 e gli altri sono caratteri per il controllo, quindi non stampabili.

**Compressione**

Sebbene tra i vari Media (audio, video,…), il testo richiede meno spazio per la sua memorizzazione, conviene intervenire con algoritmi di compressione soprattutto quando aumenta il numero dei testi da archiviare.

La compressione effettuata sul testo è **LOSSLESS** (senza perdita): la decompressione ottiene esattamente l’oggetto originario.

La compressione sul testo è giustificata dal fatto che:

1. Alcuni caratteri appaiono più frequentemente rispetto ad altri.
2. Alcuni gruppi di caratteri appaiono molto frequentemente.

Metodi noti impiegati per la compressione:

* Huffman
* Run length
* Lempel‐Ziv‐Welch (LZW)

##### Huffman

1. E’ basato sull’analisi statistica del dato da comprimere, in particolare sulla frequenza con la quale si ripetono i suoi elementi.
2. Ha una prestazione proporzionata alla varianza delle frequenze con cui compaiono i caratteri del testo da comprimere (maggiore varianza -> maggiore prestazione)
3. Utilizzabile in combinazione con altre tecniche.

*Esempio di utilizzo*

![Compressione metodo Huffman fase 1](/static/img/hoffman1.png "Compressione metodo Huffman fase 1")

![Compressione metodo Huffman fase 2](/static/img/hoffman2.png "Compressione metodo Huffman fase 2")

![Compressione metodo Huffman fase 3](/static/img/hoffman3.png "Compressione metodo Huffman fase 3")

![Compressione metodo Huffman fase 4](/static/img/hoffman4.png "Compressione metodo Huffman fase 4")

**Importante!**

Il codice di Huffman è univocamente decifrabile, non c'è possibilità di ambiguità, ogni parola non è prefisso di un altra.

##### RUN-LENGHT

RUN-LENGTH è un metodo di compressione lossless che riduce le ripetizioni di caratteri, sostituendo un RUN (insieme di caratteri ripetuti) con il carattere che viene ripetuto e con la lunghezza del RUN.

**RUN:** insieme di caratteri ripetuti.

**Lunghezza RUN:** lunghezza della ripetizioni.

> Sc | X | C

*Sc = carattere speciale per l’identificazione della codifica*

*X = il carattere che viene ripetuto nel RUN*

*C = numero di ripetizioni del carattere.*

Prestazioni buone per **run-length > 3**

*Esempio:*

"eeeeeeetnnnnnnnn" --> @e7t@n8

##### Codifica LZW

É un metodo di compressione lossless che sfrutta la ripetizione di gruppi di caratteri o frasi.

Prestazioni buone per input di testo con molte ripetizioni: linguaggio naturale (inglese, italiano,…).

##### L'Audio

L'audio è causato dalle variazioni di pressione dell'aria, le frequenze udibili dall'uomo variano nell'intervallo di **20-20.000 Hz,** ciò che descrive un onda sonora sono due descrittori :