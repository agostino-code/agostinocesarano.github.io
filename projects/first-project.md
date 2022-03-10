---
title: Laboratorio Progammazione
emoji: 😺
metaDescription: 
date: 2019-01-01T00:00:00.000Z
summary: Creare un Social Network in C.
tags:
  - C
  - Laboratorio Progammazione
---

### Task

Per la creazione del nostro Socialnetwork in C, intitolato SOCIALIZZIAMO, abbiamo da subito pensato di ricreare un Social che si avvicinasse il più possibile all’esperienza utente dei social più moderni. Prima dell’approccio con il codice abbiamo pensato a ciò che serve ad un Social per essere effettivamente usabile ed abbiamo capito che il grande limite del C è che si, praticamente si poteva creare un social usabile e del tutto funzionante ma una volta chiuso il nostro eseguibile effettivamente i dati immessi dall’utente venivano dispersi. Questo limitava tanto l’idea del social poiché un qualsiasi altro utente che avrebbe aperto quell’eseguibile non avrebbe appunto “Socializzato” con l’utente che prima ha usato quel programma. È da lì viene l’idea di lavorare con dei file, approccio fattibile in C ma comunque laborioso e rischioso per quelli che erano i tempi di consegna, anche perché mai fatto prima. Se sto scrivendo questa relazione è perché qualcosa di concreto è uscito fuori, e da una semplice idea si è creato il vero è proprio codice.

### Solution

**La questione file e strutture dati**
Prima della scelta della struttura dati da scegliere per contenere i dati che ci serviranno per la gestione di account e post, la problematica vera era su come appunto scrivere su file i nostri dati. In questo caso è bastata una semplice ricerca per venire a conoscenza delle funzioni fwrite e fread che permettono di scrivere e leggere in binario un qualsiasi blocco dati su file.
Un file binario permette di memorizzare dati di qualsiasi tipo anche vettori e strutture.
Sapendo ciò abbiamo capito che anche con una struttura, semplice come il Record, era possibile creare il nostro programma.
Infatti, la funzione fwrite scrive il record nel file e la funzione fread legge uno ad uno i record memorizzati in file e restituisce uno finché non ci sono più record nel file.

**Gestione degli account e dei post**
Per questione di praticità è per non incorrere ad errori, abbiamo deciso di creare due strutture record, uno che contiene gli account e un'altra, che contiene i post, ognuna di essi salvata appositamente in un file (data.txt per gli account, post.txt per i post).
I file dovranno essere nella directory dell’eseguibile è se trovati, il programma li apre; nel caso in cui i file non siano presenti, saranno generati automaticamente.
ATTENZIONE! In allegato con l’eseguibile ci sono due file data.txt e post.txt che contengono già file e post.

**Github:** https://github.com/agostino-cesarano/LP-Project