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