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

![](/static/img/breadth-.png)