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

**Indicizzazione su istogramma di colore. Confronto tra immagini.**

Dobbiamo definire una metrica di misurazione per stabilire quanto un’immagine è simile ad un’altra immagine.

Il processo che viene effettuato sarà quello di misurare inizialmente l’immagine di input col
suo istogramma di colore facendo poi un confronto con le immagini presenti nel db e i loro istogrammi per stabilire quale di esse corrisponde o si avvicina di più all’immagine fornita in input tramite la query.

Per la ricerca delle immagini nel DB serve definire una misura di distanza tra l’istogramma dell’immagine query e quelli delle immagini contenute nel database.

Date 2 immagini A e B, la misura di distanza più semplice è data da:

![Confronto istogrammi](/static/img/confronto-istogrammi.jpg "Confronto istogrammi")

Quindi effettuiamo una differenza tra i pixel dell’immagine A e quelli dell’immagine B, relativi al bit iesimo. Questo per ogni bin dell’immagine.

**Problemi relativi all’indicizzazione tramite istogramma del colore: problema dei bins e similarità**

La discretizzazione dello spazio dei colori in classi (bins) non tiene conto della similarità dei colori:

* Due bins adiacenti vengono considerati totalmente diversi.
* Il posizionamento della linea di demarcazione tra i bins influisce fortemente sull’istogramma e sul calcolo della distanza.
* La rappresentazione dei colori non è univoca:

  * Dipendenza dal sistema di rappresentazione
  * Dipendenza dal «device»

Quindi il confronto per istogrammi non è sempre funzionale.

**Limiti dell’approccio Color-Based: background**

Mascheramento dell’immagine ad opera dello sfondo.

Gli istogrammi sono fortemente condizionati dalla presenza di grandi blocchi di colore omogeneo e risulta che le immagini che contengono un oggetto in primo piano siano trattate in maniera errata in quanto nell’istogramma i pixel dello sfondo (background) sono maggiormente rappresentati e “mascherano” l’oggetto in primo piano.

**Come si risolve questo problema?**

Si possono usare tecniche di segmentazione (automatiche o semi‐ automatiche) per suddividere le
immagini in soggetto e sfondo e, quindi, calcolare separatamente i due istogrammi usandoli
singolarmente.

##### Indicizzazione e Ricerca basate sulla forma

Si basa su algoritmi di segmentazione delle immagini che sono in grado di suddividere una immagine in singoli oggetti attraverso metodi automatici o semiautomatici.

I sistemi efficienti devono avere una rappresentazione unica dell’immagine, invariante rispetto a traslazione, rotazione o scala.

L’immagine può essere ruotata, scalata e traslata o tutte e tre (rototraslata e poi scalata).

L’immagine però rimane sempre la stessa. 

*Dobbiamo essere capaci di analizzare la forma dell’immagine attraverso tecniche di segmentazione comprendendo che l’immagine può fare match anche se alterata rispetto alla forma.*

![Indicizzazione in base alla forma](/static/img/indicizzazione-forma.png "Indicizzazione in base alla forma")

**Definizioni geometrie degli oggetti**

* **ASSE MAGGIORE**: segmento che congiunge i due punti della forma che sono più distanti fra di loro.
* **ASSE MINORE**: segmento perpendicolare all’asse maggiore e tale che il rettangolo il cui lati sono paralleli ai due assi racchiuda completamente l’intera forma.
*  **RETTANGOLO DI BASE**: il rettangolo descritto nella precedente (esso coincide con il più piccolo
  rettangolo che contiene l’intera figura)
* **ECCENTRICITA’**: rapporto tra la lunghezza dell’asse maggiore e la lunghezza dell’asse minore

![Eccentricità immagini](/static/img/eccentricità.jpg "Eccentricità immagini")

**Normalizzazione rispetto alle rotazioni**

Il problema è che la figura potrebbe avere anche delle traslazioni: non si memorizzano nel db anche le figure traslate.

> Quello che si fa è riformulare la query, si effettua una trasformazione sulla query stessa che viene riproposta quindi per la seconda volta per intercettare l’immagine traslata.

**Normalizzazione rispetto ai cambiamenti di scala**

Quando abbiamo una figura da confrontare con un’altra converrebbe subito *normalizzare l’immagine da confrontare (renderla in forma canonica)*: 

Una volta individuato il minimo rettangolo di base contenente l’immagine è possibile effettuare una normalizzazione di scala ridimensionando tutte le forme presenti nel DataBase in modo tale che abbiano tutte lo stesso asse maggiore.

![Normalizzazione rispetto alla scala](/static/img/normalizzazione-scala.jpg "Normalizzazione rispetto alla scala")

**Calcolo della similarità**

**FASE 1:** Eccentricità molto diverse → Se due forme hanno eccentricità molto diversa tra di loro,
allora non c’è alcun bisogno di calcolare la similarità in quanto possiamo assumere che, di
conseguenza, le figure siano molto diverse.

**FASE 2:** Eccentricità uguale o simile → Se due forme hanno uguale eccentricità (e quindi la loro
stringa binaria ha uguale lunghezza), la similarità tra di loro si calcola come differenza tra rappresentazione binaria delle due immagini.

**Indicizzazione e recupero dei video**

Il video è uno dei media più complessi.

**Segmentazione**

Segmentare un oggetto informativo significa dividere l’oggetto in diverse parti usando un criterio di divisione che rispetti la natura dell’oggetto.

Per rispettare la natura del video il criterio di suddivisione deve essere basato sul contenuto del video (es. per una partita di calcio abbiamo scena del gol, del calcio d’angolo e così via..).

> Tipicamente per il video la suddivisione può avvenire quando c’è un cambio di camera infatti può rappresentare il fatto che si inquadrano scene diverse.

**Indicizzazione e ricerca video**

Il Video è ricco di informazioni in quanto è spesso corredato di:

* Sottotitoli (testo)
* Colonna sonora (audio parlato e/o musica)
* Frame (immagini catturate e riprodotte a velocità costante),
* Metadati (titolo, autore, produttore, ecc…).


Un video è costituito quindi da diverse “piste informative” per tanto è possibile usare una pista
informativa per segmentarne un’altra. 

Possiamo ad esempio usare la traccia audio per segmentare un video, non guardando i fotogrammi del video ma seguendo la traccia audio e segmentandola in corrispondenza di parole rilevanti che quindi ci permettono di individuare anche la scena video corrispondente (es. nella partita di calcio quando lo speaker grida “gol” tagliamo l’audio pochi secondi prima e dopo l’urlo ed in corrispondenza nella traccia video avremo individuato anche la scena del gol).

**Retrival per singolo fotogramma**

Il video viene considerato come una serie di immagini indipendenti su cui è possibile applicare tecniche per immagini.

Tipicamente su un secondo di tempo ci sono 25 fotogrammi, il cui scorrimento rapido ci da idea di fluidità.

Essi servono per mantenere l’immagine sul nostro occhio (persistenza dell’immagine sulla retina) ma sarebbe impossibile analizzarli tutti dato che ne sono molti e tra un fotogramma e l’altro il contenuto non varia di molto.

Conviene distanziare i fotogrammi di un certo tempo, a meno che non ci interessi un particolare frame.

Questo approccio dunque comporta evidenti svantaggi:

* perdita di informazioni temporali
* la mole di dati da elaborare è molto grande


**Retrival per gruppi di fotogrammi**

I frame vengono suddivisi in gruppi (shots) e l’indicizzazione è basata sui frame rappresentativi di ogni shot.


I migliori risultati derivano combinando due o più metodi.

**Indicizzazione e ricerca basata sugli SHOT**

Lo SHOT è gruppo di frame contigui che hanno uno o più delle seguenti caratteristiche:

* Frame fanno parte della stessa scena
* Frame non sono interrotti da uno “stacco” della telecamera
* Frame contengono lo stesso evento / azione

Per individuare i vari SHOT che compongono un video sono necessarie tecniche di segmentazione automatiche.

**Segmentazione automatica**

I frame consecutivi che sono ubicati prima e dopo un “cambio di camera” generalmente mostrano un elevato cambiamento quantitativo nel loro contenuto.

Per individuare gli shot occorre definire una misura quantitativa che catturi la differenza tra una coppia di frame:

> Data una certa soglia, se la differenza tra un frame e il successivo supera tale valore, il punto viene considerato una interruzione tra shot diversi.

Preso il fotogramma i è confrontandolo con il successivo i+1, se c'è una grande differenza tra i due frame si divide lo SHOT.

**Differenza tra frame**

Per verificare eventuali passaggi tra shot occorre misurare la differenza tra 2 frame consecutivi.

**Metodo 1:** si calcola la somma, pixel per pixel, delle differenze tra i 2 frame consecutivi.

Questo metodo non garantisce buoni risultati poiché la presenza di oggetti in
movimento causa grandi differenze anche all’interno della stessa scena e porta a
ottenere molte false interruzioni di shot.

**Metodo 2:** si calcola la differenza tra gli istogrammi di colore dei 2 frame consecutivi.

Il metodo è basato sul fatto che il movimento di oggetti all’interno della stessa scena
causa piccole variazioni nell’istogramma dell’immagine ma non così significative da
determinare un cambio di shot

*Se le metodologie adottate “scoprono” grosse variazioni allora probabilmente si tratta di un cambio di scena.*