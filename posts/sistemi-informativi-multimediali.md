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

Codifica di Huffman con la frase in francese *“Here’s an example of optimized Huffman coding using the French subject string j’aime aller sur le bord de l’eau les jeudis ou les jours impairs“*, contando i vari caratteri possiamo scriverci la frequenza di ogni simbolo (ad esempio la lettera *J* si ripete 3 volte, la lettera *a* si ripete 4 volte e così via).

Mettendo in ordine crescente la frequenza dei simboli, ad ogni passo prendiamo i caratteri con frequenza minore e li uniamo in un albero fino ad aggiungere ogni carattere del testo.

![Compressione metodo Huffman fase 1](/static/img/huffman1.gif "Compressione metodo Huffman fase 1")

Completato l’**albero di Huffman**, a partire dal nodo radice si assegna al ramo sinistro il codice 0 e al ramo destro il codice 1.

Ogni lettera del testo verrà codificata dai codici dato dal percorso dell’albero dalla radice fino al nodo che contiene la lettera. Ad esempio nell’immagine sottostante possiamo dedurre che la lettera *a* viene codificata con il codice *0110*, la lettera *e* con il codice *100* e così via.

![Compressione metodo Huffman fase 2](/static/img/huffman2.png "Compressione metodo Huffman fase 2")

Da questi esempi possiamo notare che le lettere con una frequenza minore sono state codificate con codici più lunghi rispetto alle lettere che si presentano più spesso nel testo.

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

* Ampiezza, descrive la forza del suono **db (Decibel)**.
* Tempo, descrive la frequenza del suono nel tempo **Hz (Herz)**.

Le capacità uditive dell'uomo non sono lineari rispetto a questi due parametri.

Ad esempio, per i suoni che vanno dalle frequenze di 1000 e 5000 Hz, abbiamo bisogno di un ampiezza minore ( meno dB ) per percepire il suono.

Questo è dovuto dal fatto che queste sono le frequenze del nostro parlato, quindi il nostro orecchio si è adeguato.

Questo cambiamento di percezione è descritto nelle **curve isofoniche**, che descrivono la quantità di decibel che servono per percepire un suono di una determinata frequenza.

![Curve isofoniche](/static/img/curve-isofoniche.png "Curve isofoniche")

**ADC (Analog to Digital Conversion)**

Quando dobbiamo trasformare un segnale audio in un file digitale, dobbiamo dividere il processo in tre fasi:

![Analogico a Digitale](/static/img/analogico-a-digitale.png "Analogico a Digitale")

1. *Campionamento*, prelievo di valori assunti dal segnale analogico ad intervalli discreti di tempo
   (gestiti da un clock) Δt.

   Il valore campionato resta costante durante il successivo intervallo di tempo. I campioni prelevati sono, in questa fase, ancora di tipo analogico assumendo pertanto un qualsiasi valore di un intervallo continuo.
2. *Quantizzazione*, processo di conversione dei valori continui in valori discreti. L’intervallo del segnale viene suddiviso in un numero fisso di sotto‐intervalli di uguale dimensione e viene  assegnato un valore. 

   Ciascun campione cade in uno specifico intervallo; quindi i valori possibili sono in numero limitato.

   La grandezza del sotto‐intervallo di quantizzazione è detto **passo di quantizzazione**.
3. *Codifica, p*rocesso di rappresentazione numerica dei valori quantizzati.

   Quanto maggiore sarà sia la frequenza di campionamento sia il numero dei livelli di quantizzazione allora tanto maggiore sarà la fedeltà del segnale digitalizzato.

**DAC (Digital to Analog Conversion)**

Quando dobbiamo trasformare il segnale digitale analogico, la codifica viene trasformata in un segnale analogico campionato.

Tramite un filtro passa-basso il segnale viene modellato per ricreare l'onda originaria, più sarà fedele la digitalizzazione, è meno sarà la perdita di dettagli rispetto al sognale d'origine.

![Digitale a analogico](/static/img/digitale-a-analogico.png "Digitale a analogico")

**Scelta della Frequenza di Campionamento**

##### Teorema di Nyquist

La Frequenza di Campionamento è strettamente dipendente dalla frequenza massima del segnale analogico da convertire; infatti il Teorema di Nyquist afferma che:

Se in un segnale analogico c’è una componente con frequenza massima pari a **f Hz** allora la frequenza di campionamento dovrebbe essere almeno **2 f Hz**.

La frequenza minima di campionamento, per non avere perdita di dati è almeno il doppio della frequenza massima raggiunta dal segnale analogico.

**Scelta della Frequenza di Campionamento**

##### Teorema di Nyquist

La Frequenza di Campionamento *è strettamente dipendente dalla frequenza massima* del segnale analogico da convertire; infatti il Teorema di Nyquist afferma che:

> Se in un segnale analogico c’è una componente con frequenza massima pari a **f Hz** allora la frequenza di campionamento dovrebbe essere almeno **2 f Hz**.

La frequenza minima di campionamento, per non avere perdita di dati è almeno il doppio della frequenza massima raggiunta dal segnale analogico.

**Scelta numero dei livelli di Quantizzazione**

Il numero Q dei livelli di quantizzazione determina la quantità b di bit
necessaria per rappresentare ciascun campione:

b=log2Q

La quantizzazione può essere anche dinamica prendendo i valori non a intervalli fissi, ma quantizziamo a intervalli variabili.

Questa tecnica è chiamata **Audio Companding.**

**Predictive Coding**

Con il Predictive Coding, anzichè codificare il valore del campione da trasmettere, *si codifica la differenza tra la predizione del valore del campione e il valore del campione attuale.*

L’efficacia del Predictive Coding si basa sul fatto che:

* campioni vicini sono significativamente correlati.
* per codificare una differenza occorre un numero inferiore di bit.

**Audio sintetico: Midi**

Ricrea perfettamente uno strumento musicale elettronicamente, non è un segnale analogico tramutato in segnale digitale, ma è un  suono ricreato digitalmente attraverso dei preset.

Il file midi contiene quindi informazioni e direttive che vengono interpretate da sistemi speciali (sintetizzatori) Hardware o Software e ne realizzano l’esecuzione.

Le direttive sono del tipo:

*Esegui la nota N con una durata T e con lo strumento S*

#### Le immagini

Tutti abbiamo una percezione diversa dei colori e dei dettagli.

Quando dobbiamo digitalizzare un immagine dobbiamo tenere conto della percezione dell' occhio umano.

**Rappresentazione dei colori**

Gli algoritmi di indicizzazione e di ricerca delle immagini devono essere basati su una
corretta *Rappresentazione dei colori.*

La luce visibile è una radiazione elettromagnetica con lunghezza d’onda tra 400 e 780 nm.

Differenti lunghezze d’onda producono differenti sensazioni di colore

![Spettro visibile](/static/img/visible-spectrum.jpeg "Spettro visibile")

Le tre proprietà fisiche delle radiazioni di colore sono:

* Luminanza (illuminazione)
* Tinta (il colore)
* Saturazione (la purezza)

**Sintesi additiva e sottrattiva**

Le radiazioni riflesse, *le radiazioni emesse da una fonte luminosa*, se mescolate producono la visione del bianco.

Il verificarsi di tale fenomeno da origine a quella che comunemente viene detta *sintesi o mescolanza additiva.*

Per convenzione si considerano 3 colori primari **RGB,** per la sintesi additiva.

Considerando il fenomeno dalla parte della radiazione assorbita, le radiazioni emesse dall'assorbimento di radiazioni riflesse sulle superfici.

Le superfici che ci appaiono colorate (per es. pittura e stampa) sottraggono alla nostra visione una parte dello spettro visibile.

Nella sintesi sottrattiva si analizza la capacità di assorbimento della luce.

Si considera il modello **CMYK**, per la sintesi sottrattiva.

![Sintesi sottrattiva e additiva](/static/img/sintesiaddesottr.jpg "Sintesi additiva e sottrattiva")

##### Le immagini digitali

Origini delle immagini digitali:

* Macchine fotografiche
* Scanner
* Fotogrammi di filmati
* Disegni elettronici

Schemi di classificazione delle immagini:

**Raster (o bitmap)**

> *Raster (= griglia)* definisce la griglia ortogonale di punti (scacchiera) che costituisce un’immagine. Ogni elemento è chiamato pixel a cui è associato un colore secondo uno specifico modello.

I modelli di memorizzazione possono essere **LOSSY o LOSSLESS.**

Le immagini Raster possono essere migliorate mediante la tecnica del **Multi-Frame,** più immagini raster compongono una singola.

**Vettoriali**

> Nella grafica vettoriale un'immagine è descritta mediante un insieme di primitive geometriche, *formule geometriche*, che descrivono punti, linee, curve e poligoni ai quali sono associabili svariati attributi.

Le immagini vettoriali si distinguono per la grande qualità e la elevata compressione, **LOSSLESS**, compressione senza perdita di qualità.ù

**Le immagini a colori**

Un modello di colore è un modello matematico astratto che permette di rappresentare i colori delle immagini in forma numerica; esistono diversi modelli:

* **RGB** (Red, Green, Blue) (a sintesi additiva, per es. monitor, TV,…)
* **CMYK** (Cyan, Magenta, Yellow, Black) (a sintesi sottrattiva, per es. stampanti,…)
* YUV (opera in ambito analogico; nato per la compatibilità tv colori con tv B/N)
* YCbCr (l’equivalente digitale della YUV; Y=Luminanza; Cb=CromaBlu; Cr=CromaRed)
* HSV (Hue, Saturation, Value)

##### Compressione immagine

Fondamenti della compressione:

1. L’occhio umano è limitato poiché non percepisce tutto ciò che è realmente rappresentato.
2. Generalmente, per ogni pixel di immagine, i punti adiacenti sono simili; la similitudine di tali punti ravvicinati costituisce la **Ridondanza Spaziale**.
3. Differentemente dai testi, non è particolarmente significativa la perdita di informazioni; la compressione a perdita è quindi ammessa.

**Tipi di Compressione**

> **Senza perdita (LossLess)** permette di ricostruire perfettamente la rappresentazione dell’oggetto originale (es. codifica di Huffman).
>
> **Con perdita (Lossy)** permette di ricostruire solo in parte la rappresentazione dell’oggetto originale.

Le tecniche “lossy” sono classificate in:

* Compressione con sottocampionamento
* Predictive Coding
* Codifica mediante trasformazione

**Compressione mediante sottocampionamento**

A causa della ridondanza spaziale (similitudine di pixel vicini), si considerano soltanto “alcuni” pixel; per esempio, si potrebbe considerare solo un pixel ogni due (sottocampionamento).

In fase di decodifica i pixel “mancanti” vengono ricostruiti approssimando i loro valori mediante una interpolazione.

È possibile raffinare questo metodo scegliendo di sottocampionare quelle componenti dell’immagine per le quali il nostro occhio è meno sensibile.

Ogni immagine può essere decomposta mediante le componenti Luminanza e Crominanza.