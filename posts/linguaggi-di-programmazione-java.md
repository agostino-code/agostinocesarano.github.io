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

##### **Garbage Collector**

La memoria allocata che non e più necessaria deve essere resa disponibile.

In altri linguaggi la de-allocazione e responsabilità del programmatore.

Java fornisce un thread a livello di sistema per tracciare l’allocazione di memoria.

Il Garbage Collector:

* ricerca e libera la memoria non più necessaria;
* è eseguito automaticamente;
* è dipendente dalle varie realizzazioni di JVM.

##### JRE (Java Runtime Environment)

La Java Runtime Environment è un sottoinsieme della JVM.

In dettaglio, è composto da:

* Class loader, che ha il compito di recuperare le classi che in compilazione la JVM richiede.
* ByteCode verifer, verifica che il codice scritto in bytecode non esegue azioni dannose per il sistema.

Successivamente passa il bytecode verificato all'interprete JVM.

**JIT** in alcune circostanze Java salva il programma già compilato per migliorare la velocità di esecuzione.

**Sicurezza**

Miglioramento della sicurezza del codice che proviene da fonti esterne.

* Il Class Loader:
  carica solo le classi necessarie per l’esecuzione del programma;
* mantiene le classi del file system locale in uno spazio di nomi separato, non sarà possibile rimpiazzare le librerie standard, poiché le classi locali sono sempre caricate per prime;
* previene il cosı detto spoofing.

Il Bytecode Verifier controlla che:

* il codice rispetti le specifiche della JVM;
* il codice non violi l’integrità del sistema;
* il codice non generi stack overflow o underflow;
* non vi siano conversioni di tipo illegali (e.g. la conversione di interi in puntatori).

##### SIntassi

Grammatica di Backus-Nour delle dichiarazioni.

A sinistra ci dice cosa dobbiamo rappresentare a destra dei : : = ci descrive la dichiarazione.

**Classi**

La sintassi per la dichiarazione di una classe è:

```
<class_declaration> ::= <modifier> class <name> {
                         <attribute_declaration>*
                         <constructor_declaration>*
                         <method_declaration>*
                         }
```

**Attributi**

La sintassi per la dichiarazione di un attributo è:

```
<attribute_declaration> ::= <modifier> <type> <name> [= <default_value>];

<type > ::= byte | short | int | long | char | float | double | boolean | <class>
```

**Metodi**

La sintassi per la dichiarazione di metodi è:

```
<method_declaration> ::= <modifier> <return_type > <name> (<parameter>*) {
                         <statement >*
                         }
```

**Accesso a membri di oggetto**

La notazione “dot”: <object>.<member>.

è usata per l’accesso a membri non privati di una oggetto.

Ricordiamo che Java ha uno scoping statico, quindi possiamo accedere agli attributi dei blocchi più esterni.

**Costruttori**

La sintassi per la dichiarazione di un costruttore è:

```
<constructor_declaration> ::= <modifier> <class_name> (<parameter>*) {
                              <statement >*
                             }
```

I costruttori non avranno tipo di ritorno è come nome hanno il nome della classe.

* I costruttori NON sono metodi.
* I costruttori non vengono ereditati dalle sottoclassi.

**Costruttore di default**

* C’è sempre almeno un costruttore in ogni classe.
* Se il programmatore non scrive nessun costruttore, allora verrà usato un costruttore di default.
* Il costruttore di default non ha argomenti.
* Il costruttore di default non ha corpo.

Il costruttore di default permette di creare istanze di classi ( con l’espressione new *nomeclasse*()) senza dover scrivere un costruttore.

**Sorgenti**

```
<source_file > ::= [< package_declaration >]
                     <import_declaration >*
                     <class_declaration >*
```

* l’ordine degli elementi e importante;
* il nome del file sorgente deve essere lo stesso dell’unica classe pubblica contenuta nel file; se il file sorgente non contiene classi pubbliche allora il nome del file può essere qualunque.

**Enunciato package**

La sintassi dell’enunciato package è:

```
<package_declaration > ::= package <top_pkg_name > [.< sub_pkg_name >]*;
```

Ricorda:

* la dichiarazione specifica che il contenuto del file appartiene al pacchetto dichiarato;
* e permessa una sola dichiarazione di pacchetto per file sorgente;
* si deve specificare la dichiarazione all’inizio del file sorgente;
* se non è dichiarato il pacchetto, allora il contenuto del file appartiene al pacchetto di default;
* i nomi di pacchetto devono essere gerarchici e separati da punti;
* un nome di pacchetto corrisponde di solito ad un nome di cartella;
* in genere i nomi di pacchetto sono scritti in lettera minuscola, mentre i nomi di classe sono in lettera minuscola ma ogni loro parola comincia per lettera maiuscola.

##### Incapsulazione

È un concetto introdotto già prima della nascita di Java è dei linguaggi ad oggetti.

**Il problema**

Dato il seguente class diagram:

  *MiaData*
+giorno : int
+mese : int
+anno : int

Il codice cliente ha accesso diretto ai dati interni:

```java
MiaData d = new MiaData ();

d. giorno = 32;
// non valido

d.mese = 2; d. giorno = 30;
// plausibile ma sbagliato

d. giorno = d. giorno + 1;
// nessun controllo del limite superiore
```

Ciò significa che non effettuo controlli sui dati, i dati hanno accesso diretto.

**La soluzione**

  *MiaData*
-giorno : int
-mese : int
-anno : int

\------------------------------------
+getGiorno() : int
+getMese() : int
+getAnno() : int
+setGiorno( g : int ) : boolean
+setMese( m : int )
+setAnno( a : int )
-validGiorno( d : int ) : boolean

Il cliente deve usare i metodi per accedere ai dati interni:

```java
MiaData d = new MiaData ();

d. setGiorno (32);
// non valido , ma ritorna falso

d. setMese (2);
d. setGiorno (30);
// plausibile ma sbagliato ; setGiorno ritorna false

d. setGiorno (d. getGiorno () + 1);
// restituisce false se si eccede il limite
```

Gli attributi saranno privati, ci saranno metodi che permettono di accedere agli attributi ed effettuano tutti i controlli del caso, rispettando i vincoli di integrità di quei attributi.

L'incapsulazione permette anche di cambiare facilmente l'implementazione, es. collection.

Rendere il codice modulare è un vantaggio enorme.