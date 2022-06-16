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

**Problema?**

Come memorizzo le caratteristiche pre-processate?

##### Inverted Files

L’inverted file contiene un insieme di record che contengono:

* il termine che si vuole cercare
* una sequenza di puntatori a documenti e/o records che contengono quel termine

La ricerca può essere effettuata tramite Operatori Booleani OR AND NOT

Query con composizione booleana delle chiavi di ricerca

*Esempio:* termine_1 ANT NOT termine_2

> Il processo di ricerca è più efficiente rispetto al **flat‐file** non si analizzano i documenti interi ma solo l’inverted file da cui si ricavano i collegamenti ai documenti che soddisfano la query.

![Inverted File](/static/img/inverted-file.png "Inverted File")

**Inverted File con operazioni estese**

È possibile raffinare la ricerca tenendo conto di:

* Differenza di importanza tra un termine e un altro.
* Posizione in cui un termine compare.
* La frequenza in cui un termine compare all’interno di un documento.

Definiamo 2 nuovi operatori di «prossimità» quali “**WITHIN SENTENCE**” e “**ADJACENT**”

> *WITHIN SENTENCE* i termini ricercati sono presenti nello stesso paragrafo del record recuperato.
>
> A*DJACENT* termini ricercati confinanti nel record recuperato.

##### Indicizzazione automatica del testo

Il processo di indicizzazione del file di testo prevede diverse fasi; lo scopo principale è quello di filtrare il testo in modo da mantenere solo le informazioni da considerare per le ricerche.

![Indicizzazione automatica testo](/static/img/indicizzazione-testo.png "Indicizzazione automatica testo")

Fasi di filtraggio:

1. **Stop Words**, si escludono elementi insignificanti per la ricerca come “articoli”, preposizioni”,…
2. **Stemming**, se nel testo compare più volte parole analoghe, per la ricerca si considera solo il
   termine comune delle parole analoghe. *Esempio:* se nel testo sono presenti i termini
   “pescare”, “pescatore”, “pesce” allora considero solo il loro prefisso comune, cioè “pesc”.
   Anche se tale operazione rende il file più compatto, d’altro canto occorre considerare che,
   per esempio, a causa della brevità del termine comune esso non sia più molto significativo.
3. **Thesaurus**, possibilità di sostituire diversi termini simili che compaiono nel testo con un
   unico termine (usando un vocabolario). Esempio: se nel testo sono presenti i termini
   “lavare”, “pulire”, “detergere” allora potrei considerare solo il termine “lavare”.
4. **Weighting,** I termini che compaiono nel testo hanno diversa importanza; la loro importanza
   può essere ricavata valutando le loro frequenze di occorrenza ed il risultato della ricerca
   viene mostrato in ordine di frequenza.

**Calcolo dei pesi**

Il peso di un termine deve considerare il numero di volte in cui il termine compare sia nel documento sia nell’insieme complessivo dei documenti.

La formula comunemente utilizzata per il calcolo dei pesi è:

> W = f * log (N/dfj)

In cui:

* W = peso del termine j nel documento i
* f = frequenza del termine j nel documento i
* N = numero totale dei documenti del DataBase
* dfj = numero dei documenti del DataBase che contengono il termine j

##### Algoritmo di pattern matching e pattern matching 2

Nell’algoritmo di pattern matching 2 spostiamo il pattern di ricerca più avanti di una casella alla volta a differenza di quello normale, ciò è possibile grazie alla particolare funzione fallimento che si costruisce partendo dal pattern di ricerca (disposizione dell' testo).

Grazie ad essa, una volta costruita se si fallisce un determinato numero di confronti non abbiamo bisogno di proseguire, poiché riusciamo a prevedere già cosa si trova in seguito che non corrisponde col pattern, quindi possiamo spostarci di n posizioni in avanti, non dovendo scorrere
tutti i caratteri.

Ciò migliora la complessità computazionale della ricerca: per l’algoritmo di pattern matching 2 equivale a **O(M+N)** e **O(M*N)** per l'algoritmo di pattern matching semplice carattere per carattere.

##### Retrival con modello vettoriale

Il “retrieval” di un documento dal database mediante il modello spazio vettoriale si basa sul calcolo del prodotto scalare tra vettori.

Supponiamo di aver formulato una query q fissata, secondo il modello del **document retrieval**. Si deve confrontarla con i documenti presenti nel database multimediale per ottenere la risposta desiderata.

Per effettuare il confronto traduciamo tutto in vettori:

in particolare traduciamo la query e ogni documento in un vettore delle caratteristiche **(features vector)**. 

Dunque ad ogni documento presente nel db associamo un vettore che rappresenta le sue caratteristiche rilevanti. 

> Il db sarà formato da **N documenti**. La **query q** deve essere confrontata con tutto il database per conoscere a quale documento fra quelli presenti nel db *“somiglia”* e si avvicina di più. Per effettuare il **confronto** tra il **vettore delle caratteristiche associato alla query** e gli **N vettori delle caratteristiche associati ai diversi documenti presenti nel database** utilizziamo il prodotto scalare.

**Richiami di geometria e fisica**

> Un vettore **è un ente geometrico** con il quale **esprimiamo graficamente grandezze fisiche**. Esso è rappresentato tramite un segmento orientato ed è definito da un modulo, una direzione, un
> verso e da un punto di applicazione.

* Il modulo è un numero che indica quanto è intensa la grandezza che viene associato al vettore.
* La lunghezza del vettore è indicata dal modulo. La retta sulla quale giace il segmento è la direzione del vettore. 
* La freccia del vettore indica il verso, ossia verso dove agisce il vettore. 
* Il punto di applicazione è il punto in cui si applica la grandezza.

Immaginiamo di avere 2 vettori a e b nello spazio le cui componenti per individuarli sono rispettivamente:

**a = \[a1, a2, …, an]**

**b = \[b1, b2, …, bn]**

Tra i due vettori si forma un certo angolo **theta θ**. Se calcoliamo **\|a| cos θ** è come se stessimo proiettando la componente di a su b: quindi **\|a| cos θ** *è la proiezione di a su b.*

> Il modulo del vettore a si calcola attraverso il teorema di pitagora

*quindi faremo la radice quadrata della somma di ciascuna componente del vettore elevata al quadrato.*

![Prodotto scalare](/static/img/prodotto-scalare.jpg "Prodotto scalare")

**Richiami Seno, coseno, circonferenza goniometrica**

Seno e Coseno indicate con sin(α) e cos(α), sono due funzioni trigonometriche fondamentali che vengono definite a partire dalla circonferenza goniometrica (circonferenza di raggio 1), e che associano a ciascun angolo un determinato valore numerico compreso tra -1 e +1.

**Richiami Teorema di pitagora**

Preso un triangolo rettangolo (un angolo del triangolo misura 90°), il teorema di pitagora definisce formule per il calcolo dei lati.

![Teorema di pitagora](/static/img/teorema-di-pitagora.png "Teorema di pitagora")

Le formule inverse permettono il calcolo dei cateti, la formula base prevede il calcolo dell'ipotenusa.

> Quindi il **Retrieval con modello spazio vettoriale** usa ilo prodotto scalare per il calcolo dell' indice di similitudine tra i vettori delle caratteristiche di Query e Documenti.

Due vettori a e b quando hanno un angolo theta che converge a 0, sono più simili;
indipendentemente dalla loro lunghezza.

Due vettori non sono per niente simili quando l’angolo fra essi compresi è di 90°.

Il coseno a 90° vale 0! Quindi i due vettori sono totalmente opposti.

Quando i due vettori sono ortogonali tra di loro i documenti sono incoerenti fra di loro.

> Quindi se i due vettori delle caratteristiche hanno l’angolo theta che si avvicina a 0 sono simili.
>
> Se hanno l’angolo theta che si avvicina a 90° sono difformi tra di loro.

##### Tecniche basate su revalence feedback

Quando scriviamo una query in un motore di ricerca non sempre abbiamo da subito il risultato desiderato.

Probabilmente dobbiamo scrivere la query più volte. Il motore di ricerca prende atto del
cambiamento: propone un raffinamento della query tramite una sorta di “contrattazione”, che fa si che quando formuliamo un ulteriore query la formuliamo via via più precisa.

> Il motore di ricerca sfrutta il feedback che l’utente stesso gli fornisce con le sue ricerca.

**Effettuiamo quindi una query modification.**
L’idea di base di questo modello consiste nello sfruttare le valutazioni degli utenti (feedback)
permettendo di raffinare i pesi dei termini sia della query sia dei documenti.

Nella query modification:

* La modifica di una query beneficia solo l’utente che l’ha formulata.
* I termini che sono stati ritenuti rilevanti vengono aggiunti alla query originale oppure viene aumentato il peso di quel termine.
* I termini che non sono stati ritenuti rilevanti vengono cancellati dalla query oppure viene diminuito il peso di quel termine.

La regola applicata è la **formula di rocchio**: la valutazione di una query si ottiene valutando la query precedente aggiungendo o sottraendo alcune componenti più significative o meno significative. 

> Raffina quindi il confronto tra documento e query, creando un nuovo vettore delle Query più "raffinato".

Il raffinamento della Query è a beneficio dell'Utente mentre il motore di ricerca attraverso la **document modification** raffina i vettori delle caratteristiche dei documenti. 

Modifichiamo il vettore delle caratteristiche di un documento in base alle query che vengono ripetute e modificate dagli utenti.

La documento modification avviene in maniera automatica (in seguito a click utente che modificano il ranking del documento) o manuale (a pagamento per agevolare il ranking, persone valutano i documenti e ne identificano le caratteristiche).

Nella document modification:

* La modifica di un documento beneficia anche altri utenti.
* I valori dei pesi dei documenti vengono aggiornati considerando la query stessa (e non considerando la lista dei documenti giudicati rilevanti dall’utente).
* Vengono aumentati i pesi dei termini che si trovano sia nella query che nell’insieme dei documenti rilevanti.
* Vengono diminuiti i pesi dei termini che si trovano nell’insieme dei documenti rilevanti ma non nella query.

##### Modello basato su Cluster

Raccogliamo in uno spazio(cluster) i documenti simili tra loro.

All’interno del cluster individuiamo l’elemento centroide ossia un elemento reale o virtuale che lo
identifica.

Il confronto della query non lo facciamo con tutti i documenti, ma con i diversi centroidi di documenti.

Fra i centroidi si sceglie quello più vicino alla query e lo si confronta con essa.

**Generazione del cluster**

**Similarità per coppie:** si costruisce una matrice delle distanze; ogni documento è
distante in termine di similarità da un altro documento e si costruisce la matrice.

Si prende la coppia di documenti con la minor distanza; la coppia viene eliminata dalla matrice e si restituisce come un unico elemento centroide che è come se fosse il centro fra i due.

Si ripete il procedimento finché la matrice non diventa di un unico elemento formando un cluster
“agglomerato di documenti”.

**Clustering euristico:** parte dall’ipotesi di aver un unico documento in un unico cluster.

Quando arriva un documento dall’esterno lo si aggiunge al cluster più similarmente vicino ad esso.

Se il documento è troppo distante dal cluster se ne forma uno nuovo.

##### Cluster-Based Retrieval

Dopo aver generato i vari Cluster, la ricerca sarà più efficace.

Data una Query, si restituiscono l'insieme di Documenti del Cluster in cui il Centroide è simile alla Query ricercata.

Il confronto avviene solo sui Centroidi è non su tutti i documenti.

##### Misurazione delle prestazioni

* Velocità di ricerca
* **Recall:** capacità di recuperare informazioni rilevanti dal database. Si
  definisce come rapporto tra il numero dei documenti rilevanti recuperati
  ed il numero totale di elementi rilevanti nel database.
* **Precisione:** misura l’accuratezza dei documenti recuperati. Si definisce
  come rapporto tra il numero di documenti rilevanti recuperati ed il numero
  totale di documenti recuperabili.

![Calcolo prestazione di un MIRS](/static/img/prestazioni-di-un-mirs.jpg "Calcolo prestazione di un MIRS")

Nella pratica, i parametri di valutazione recall e precisione vengono valutati in modo congiunto, ed una buona prestazione è indice di compromesso.

**Tipicamente quanto maggiore è la recall tanto minore risulta la precisione:** infatti quanto maggiore è lo sforzo della query per prelevare tutti i documenti rilevanti, tanto maggiore sarà la probabilità che in output andranno anche documenti non rilevanti (e quindi imprecisione).

**Viceversa quanto maggiore è la precisione tanto minore risulta la recall:** per evitare di prendere elementi non rilevanti si finisce inevitabilmente per non prelevare qualche documento rilevante.

##### Indicizzazione e recupero dell’audio

Per ciò che riguarda l'audio non esiste uno standard per l'indicizzazione.

Non c’è un metodo generale che permetta di definire quale sia lo standard.

Per gli esseri umani risulta semplice saper distinguere tra:

* differenti tipi di audio (voce, musica, rumori,…)
* diverse “velocità di esecuzione” (lento, svelto,…)
* diversi toni (felice, arrabbiato, triste,…).

Inoltre, per un essere umano, risulta semplice determinare la similitudine tra diversi pezzi audio.

Attualmente, il modo più utilizzato per classificare vari brani audio è basato sul titolo oppure sul nome del file.

Tale metodo rende impossibile ricercare tramite query come “cercare un brano audio simile a quello che abbiamo appena ascoltato”.

Ulteriore complicazione nasce dal fatto che non esiste uno standard di memorizzazione del file audio (diverse frequenze di campionamento, ampiezze,….) e ciò comporta ovviamente grosse problematiche per il loro confronto.

Risulta pertanto necessario sviluppare tecniche e metodi di retrieving diverse.

**Approccio generale per l’audio indexing**

L’approccio che viene generalmente seguito per lo studio dei vari brani audio consiste nel realizzare un primo livello di distinzione:

* Parlato
* Musica
* Rumori

La gestione è quindi diversificata per tipologie: per esempio nei file audio, lo studio del parlato (speech recognition) consiste principalmente nel convertire il file audio parlato in parole di testo su cui si potrà poi effettuare una query tradizionale.

Le query audio vengono gestite su sottoinsiemi simili di brani audio.

La distinzione tra diverse tipologie audio è importante per diverse ragioni:

* Diversi tipi di audio richiedono differenti tecniche di indicizzazione e recupero
* Diversi tipi di audio assumono significati diversi per le applicazioni
* La classificazione comporta poi una riduzione dello spazio di ricerca

**Proprietà e caratteristiche principali dell’audio**

Del segnale audio possiamo avere una rappresentazione:

> Nel dominio temporale \[time domain] (rappresentazione Tempo/Ampiezza)

l’asse X rappresenta il tempo, l’asse Y rappresenta l’ampiezza del segnale

> Nel dominio delle frequenze (rappresentazione Frequenza/Magnitudine)

Es. La voce arriva ad una frequenza di 7K

**Si passa dal dominio temporale a quello frequenziale utilizzando la trasformata di Fourier.**

Ciascun tipo di rappresentazione è particolarmente idonea per l’estrazione di determinate
caratteristiche.

##### Caratteristiche derivabili dal Time Domain

La rappresentazione Time Domain è la tecnica più immediata ed intuitiva per la rappresentazione di un segnale la cui ampiezza varia nel tempo.

Dal time domain possiamo ricavare il silenzio ossia un parametro rappresentato dallo 0.

I valori del segnale possono essere positivi o negativi a seconda se la pressione d’aria provocata dall’onda sonora risulta essere superiore o inferiore alla pressione atmosferica in condizioni di silenzio.

Si assume che ogni campione audio sia rappresentato mediante un insieme di 16 bit; ciò comporta che il campionamento dei valori da 32767 (2^15‐1) a ‐32767.

**Average Energy (energia media)**

Rappresenta l’energia complessiva che un certo segnale esprime, dovuta all’intensità con la quale viene espresso un suono.

* Più è alta è l’ampiezza del segnale audio più elevata l’intensità.
* Indica la “rumorosità” del segnale audio

**Zero crossing rate**

Frequenza di passaggio per lo zero. Indica con quale frequenza cambia segno l’ampiezza del segnale.

**Silence Ratio (Quantità di silenzio)**

Indica la proporzione di silenzio nel brano musicale; è il periodo entro il quale i valori
assoluti di ampiezza di un certo numero di campioni (e non solo un singolo valore) e per un “certo” tempo siano prossimi allo zero.

##### Caratteristiche derivanti dal Dominio delle Frequenze

La rappresentazione nel dominio delle frequenze deriva dalla rappresentazione nel dominio temporale applicando la trasformata di Fourier.

La trasformata di Fourier decompone un segnale nelle proprie frequenze componenti.

Nel Dominio delle Frequenze il segnale viene rappresentato come ampiezza che varia in base alla frequenza; in altre parole tale rappresentazione mostra in che modo è distribuita l’energia alle varie frequenze.

> La rappresentazione nel dominio delle Frequenze è comunemente detta **Spettro del segnale**

![Spettro del segnale](/static/img/spettogramma.png "Spettro del segnale")

*Colore più intenso indica una ampiezza maggiore.*

##### Bandwidth (Larghezza di Banda)

Gamma (o range) delle frequenze di un suono.

*Es. Mediamente la musica ha un range molto più ampio del parlato*

Il metodo più semplice adottato per il calcolo del range effettua una differenza:

> Range frequenze = Max. Frequenza - Min. Frequenza

Lo spettro del segnale facilita la valutazione della distribuzione delle frequenze componenti; ad esempio è possibile rapidamente valutare se il segnale possiede componenti con frequenze elevate.

* La presenza di alte frequenze nel segnale audio comporta che con alta probabilità il segnale in oggetto contiene musica (la musica ha frequenze molto più elevate rispetto il parlato).
* **7kHz è la soglia del parlato:** se facciamo un’analisi e notiamo che la frequenza non supera i 7kHz allora già possiamo stabilire che il segnale audio non rappresenta musica ma parlato.

Ciò non è possibile nel dominio temporale, ma solo in quello frequenziale.

> Frequenze fino a 7 kHz banda bassa; frequenze oltre i 7 kHz banda alta.

**Armoniche**

Un suono prodotto da un corpo vibrante non è mai puro, ma è costituito da più segnali più acuti e meno intensi, questi sono gli armonici, che hanno una importanza fondamentale nella determinazione del timbro di uno strumento e nella determinazione degli intervalli musicali.

> Le armoniche di un suono sono multiple in frequenza rispetto una frequenza più
> bassa detta frequenza fondamentale.

In genere la musica contiene molte più armoniche di un semplice suono

Il test che stabilisce se un suono contiene armoniche controlla che le frequenze di componenti dominanti siano multiple di una frequenza fondamentale.

##### Riconoscimento del parlato

> Lo *automatic speech recognition (ASR*) prende in input un segnale audio e restituisce un testo, il quale viene indicizzato e ne recupera le caratteristiche.

**Tecniche basate sul Dynamic Time Warping (DTW)**

Ogni “pezzetto” di parlato (frame temporale per esempio di 10 ms) viene rappresentato da un vettore P di caratteristiche.

Il processo di riconoscimento consiste nel considerare più piccola delle differenze tra il vettore P e ciascun vettore memorizzato nella precedente fase di Training.

**Dynamic Time Warping**

Quando abbiamo un’onda che esprime un certo segnale da riconoscere, non abbiamo mai la corrispondenza diretta con un altro: dobbiamo trovare un modo per sovrapporre i segnali.

Dobbiamo estrarre delle caratteristiche dal segnale che ci consentano di riconoscerlo.

> Col DTW dobbiamo fare una sorta di “stretching” del segnale sull’asse del tempo, per estenderlo, in modo da farlo coincidere con un altro segnale.
>
> In particolare facciamo corrispondere i picchi del segnale.

*Quindi se abbiamo un segnale dove devo riconoscere il parlato, da confrontare con un altro segnale già riconosciuto, ma con un parlato più veloce, o più lento, posso effettuare la contrazione o la dilatazione del segnale nell'asse del tempo per far combaciare i picchi.*

![Time Warping](/static/img/time-warping.jpg "Time Warping")

**Altri usi dell' Dynamic Time Warping**

Con il Time Warping possiamo effettuare il riconoscimento di una firma basata sull’abbinamento e sul confronto di punti significativi della
firma di riferimento e quella da verificare.

Per sapere se le firme sono uguale prendiamo una serie di punti e cerchiamo di trovare una serie di corrispondenze tra le due.

![Signature verification](/static/img/signature-verification.png "Signature verification")

Alcuni esempi di applicazione del Time Warping sono::

* Riconoscimento del parlato (speech recognition)
* Riconoscimento della scrittura (handwriting and online signature matching)
* Riconoscimento dei gesti (gesture recognition)
* Allineamento delle sequenza di proteine
* Musica ed elaborazione di segnali

**Prestazione dei Sistemi di Speech Recognition**

Le prestazioni dei Sistemi di Speech Recognition sono influenzate dai seguenti fattori:

* Soggetto del parlato: articolo di giornale, libro tecnico, ecc…
* Tipo di parlato: letto o conversazione spontanea
* Dimensione del vocabolario utilizzato

**Tecniche di identificazione dello speaker**

Si tenta di riconoscere non solo il contenuto del parlato (speech recognition) ma anche lo speaker,
attraverso tecniche come reti neurali.

Cercano di estrarre informazioni su chi sta parlando ed alcuni degli obiettivi sono:

Identificazione del numero di speaker che stanno parlando

Identificazione del sesso o dell’età dello speaker

Identificazione dello stato emotivo o attitudinale (allegro, triste, ecc…)

Riconoscimento della persona che sta parlando (Voice Recognition)

Utilizzano un approccio contrario ai metodi di Speech Recognition (i quali devono essere speaker‐independent e quindi cercano di eliminare le caratteristiche peculiari del parlato di ognuno degli
speaker) cercando di enfatizzare le differenze di pronuncia, linguistiche e temporali tra i vari speaker.

**Relazioni tra audio ed altri media**

Quando bisogna fare il riconoscimento di un filmato è sbagliato fare un riconoscimento solo sulla parte video del filmato (la più complessa).

Se all’interno di una sequenza multimediale complessa dobbiamo riconoscere una determinata sequenza, facciamo l’analisi dell’audio.

Possiamo segmentare la traccia video in base all’audio.

> Segmentare significa suddividere un oggetto rispettando la sua natura e il significato delle sue parti. 

Facciamo corrispondere la segmentazione audio a quella video: saranno tra loro sincronizzate.

In molte applicazioni l’audio è parte di un oggetto multimediale composito (ad esempio un film) dove esistono delle forti relazioni temporali tra video ed audio.

Possiamo utilizzare la conoscenza su uno dei media per migliorare l’indicizzazione e la comprensione del contenuto dell’altro media, quindi individuando delle caratteristiche audio, possiamo capire cosa viene mostrato in video.

##### Indicizzazione e recupero delle immagini

L’indicizzazione ed il recupero delle immagini costituisce un settore di ricerca in cui si sono raggiunti risultati molto importanti e avanzati.

I risultati ottenuti in questa di ricerca sono spesso sfruttati nei database relazionali di tipo commerciale.
Tecniche usate spesso in: google photos, amazon photos, flickr. 

Ad esempio in google foto se cerchiamo “bottiglia” ci propone tutte le immagini che dentro contengono bottiglie, perché fa un’analisi e le trova.

Google foto va oltre la classificazione delle foto “per evento”. Fa classificazioni automatiche.

Le principali tecniche di indicizzazione sono:

![Indicizzazione delle immagini](/static/img/indicizzazione-foto.jpg "Indicizzazione delle immagini")

**Memorizzazione di attributi strutturati**

Questa strategia è fondata sulla memorizzazione di informazioni per ognuna delle immagini del D.B.M.S. dei cosiddetti Meta-Dati :

> Nome del file, Data di creazione, Autore, Categoria dell’immagine, Soggetto.

L’indicizzazione e la ricerca possono quindi essere effettuate con tecniche standard dei DBMS.

I limiti più evidenti di questa metodologia sono:

* Gli attributi possono non descrivere in maniera completa le immagini
* Le query sono limitate ai soli attributi memorizzati

Riconoscimento degli oggetti (computer vision)

Questa strategia è fondata su sofisticate tecniche di estrazione di feature e di algoritmi di riconoscimento degli oggetti presenti nella scena.

Caratteristiche principali:

* Sono computazionalmente molto pesanti
* Richiedono algoritmi estremamente sofisticati
* Godono di una buona prestazione solo per domini applicativi ristretti
* Sono argomento di ricerca avanzata (Computer Vision)

In queste tecniche il sistema deve riconoscere in modo automatico tutto ciò che c’è nella fotografia e in qualche modo deve tirare fuori una serie di elementi che costituiranno il features vector che ci permetterà di fare il retrieving dell’immagine.

*Lo svantaggio è la grande capacità di computazione richiesta.*


Tecniche di utilizzo specifiche:

* Tecniche di riconoscimento del viso si dicono tecniche biometriche che ci permettono di riconoscere una persona attraverso la distanza degli occhi forma del viso ecc.
* Altro esempio di riconoscimento immagini è il sistema che rileva il numero di targa, tutor.

**Annotazioni libere (Text-based image retrieval)**

Le immagini sono descritte con testo libero (non controllato).

La ricerca usa gli algoritmi convenzionali di IR (Information retrieval) basati sulla ricerca di similarità tra query e testo descrittivo delle immagini.

Essendo una tecnica “manuale”, occorre notare che:

* Il testo deve essere il più possibile completo e consistente
* Il testo introdotto potrebbe essere soggettivo e occorre utilizzare tecniche di relevance feedback

I vantaggi sono che si possono “catturare” anche concetti di alto livello (cioè astratti) presenti nell’immagine che possono essere captati solo dall'uomo.

Questo però richiede che un uomo descrivi ogni immagine, perdiamo quelli che sono gli automatismi dell'indicizzazione.

**Estrazione di feature di basso livello**

L’estrazione di feature di basso livello è definita su tecniche di indicizzazione e ricerca basate sul
contenuto (content‐based).

Possono prendere in considerazione una o più delle seguenti caratteristiche:

* COLORE
* FORMA
* TEXTURE: immagine che si ripete, zone di riempiemento che si ripetono

**Algoritmi basati sull’analisi del colore: istogramma di colore**

Ogni immagine è memorizzata assegnando ai pixel tre valori numerici ad ognuno dei canali di colore (ad esempio RGB).

Ogni canale è campionato in m intervalli (quantizzazione dei colori): il numero totale di combinazioni diverse (bins) è m al cubo. (es: 16 intervalli di colore 4096 bins)

> Si definisce ISTOGRAMMA di COLORE la curva permette di capire come sono distribuiti i colori all’interno dell’immagine.


Un’immagine rgb può essere caratterizzata da 3 istogrammi di colore:

uno che rappresenta la distribuzione dei blu, uno dei verdi e uno dei rossi.


Se per ogni pixel dell’immagine scegliamo di rappresentare la sfumatura di quel pixel con 1 byte significa che per 8 bit ho 2^8 = 256 valori possibili toni di grigio (lo 0 rappresenta il nero  255 è il bianco).


I bins sono quantizzazioni dell’intervallo di valori che può assumere un pixel (da 0 a 255).

Possiamo suddividere quindi l’intervallo di colori possibili in 255 parti, chiamate bins.

**Confronto degli istogrammi di immagini**

![Istogramma di colore](/static/img/instogramma-di-colore.jpg "Istogramma di colore")

In questo caso decomponiamo l’immagine nello schema RGB, attraverso l’istogramma dei blu, dei verdi e dei rossi.

![Istogramma e contrasto](/static/img/istogramma-e-contrasto.jpg "Istogramma e contrasto")

Diverse tipologie di contrasto applicate sulla foto originale producono alcuni cambiamenti sull’istogramma iniziale dell’immagine.

Con un basso contrasto addensiamo tutti i puntini dell’immagine intorno ad una stessa parte, non ci sono punti estremi, man mano che il contrasto si abbassa più la punta diventerà alta fino al
caso massimo in cui il contrasto è nullo e vedremo un’unica tinta.


Con alto contrasto si vengono a creare dei punti di accumulazione con addensamento di valori,
più il contrasto diventa elevato più tutto si addensa intorno a pochi colori.

Con bassa o alta luminosità l’istogramma non si deforma, esso viene semplicemente traslato
verso sinistra o destra.

* alta luminosità: quando aumentiamo la luminosità l’istogramma di colore viene traslato verso destra verso toni più chiari
* bassa luminosità: quando diminuiamo la luminosità l’istogramma di colore viene
  traslato verso sinistra verso toni più scuri