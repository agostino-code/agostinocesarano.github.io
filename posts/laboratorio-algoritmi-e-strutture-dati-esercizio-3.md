---
title: Laboratorio Algoritmi e Strutture Dati (Esercizio 3)
date: 2022-06-20T06:50:28.471Z
author: Agostino Cesarano
summary: Appunti per il corso di LASD, Professore Mogavero; esercizio numero 3, alberi.
tags:
  - LASD
---
##### Iteratori

L'iteratore è un algoritmo che permette lo scorrimento dell'albero, in base a quello che sarà l'ordine di visita dell'albero possiamo identificare un iteratore:

**PreOrder**

La visita preorder, partendo dalla radice visita prima la radice, per poi visitare i suoi sottoalberi.

![Visita pre order](/static/img/pre-order.png "Visita pre order")

**InOrder**

La visita inorder, partendo dalla radice, visita prima il sottoalbero sinistro, partendo dal nodo "più a sinistra" , nel caso di un *albero binario di ricerca* visitiamo l'albero in ordine di "grandezza".

![Visita in order](/static/img/in-order.png "Visita in order")

**PostOrder**

La visita postorder, partendo dalla radice, visita prima i sottoalberi, in ultimo la radice.

![Visita post order](/static/img/post-order.png "Visita post order")

**Breatdh**

La BFS Breadth-First Search è un algoritmo di visita che partendo dalla radice, visita tutti i livelli dell'albero in ampiezza.

![Visita in ampiezza](/static/img/breadth-.png "Visita in ampiezza")

Gli iteratori sono composti da due componenti principali,

* l'operatore di accesso *
* l'operatore di incremento ++

L'operatore di accesso accede al dato visitato, mentre l'operatore di incremento visita il nodo successivo.

Appena istanziamo l'iteratore, visitiamo il primo nodo della sequenza di visita.

**Come implemento gli iteratori?**

Per quanto riguarda le visite, gli iteratori usano strutture dati ausiliari, le visite pre-post-in order usano, lo stack.

Mentre la visita Breatdh usa una queue, coda.

**Resettable Iterator**

Le nostre implementazioni, hanno anche una funzione di reset, che azzera l'iteratore; l'iteratore viene posto nello stato iniziale.

##### Implementazione dell'albero

Le implementazioni possibili dell'albero, sono due, una possibile tramite puntatori e l'altra possibile tramite vettore.

**Implementazione tramite vettori**

L'implementazione tramite vettore è possibile seguendo queste tre regole:

* se il nodo è la radice allora v va in posizione 1 (nel vettore sarà posizione 0),
* se il nodo v è figlio sinistro del nodo u allora la posizione di v è p(v) = 2*p(u),
* se il nodo v è figlio destro del nodo u allora la posizione di v è p(v) = 2*p(u) + 1;

**Implementazione tramite puntatori**

L'implementazione tramite puntatori prevede che ci sia una struttura ausiliaria, che contiene:

* il valore che il nodo deve assumere,
* il puntatore alla struttura nodo, che figura il nodo sx,
* il puntatore alla struttura nodo, che figura il nodo dx;