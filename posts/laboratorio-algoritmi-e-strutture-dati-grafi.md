---
title: Laboratorio Algoritmi e Strutture Dati (Grafi)
date: 2022-06-23T00:27:25.069Z
author: Agostino Cesarano
summary: Appunti per il corso di LASD, Professore Mogavero; grafi.
tags:
  - LASD
---
**Codifica di un Grafo**

Un grafo G è una coppia di insiemi (V, E) dove V è un insieme finito e non vuoto e E ⊆ V×V è un sottoinsieme del prodotto cartesiano di V.

Chiamiamo gli elementi dell’insieme V vertici mentre quelli dell’insieme E archi.

La codifica di un grafo è possibile mediante due rappresentazioni:

* Matrice di adiacenza
* Lista di adiacenza

##### Matrice di adiacenza

Creo una matrice i x j, ogni cella rappresenta una coppia di vertici M(Vi,Vj).

Ogni cella avrà valore 1 se la coppia di vertici è associata con un arco, quindi la coppia appartiene all'insieme E.

Altrimenti avrà valore 0.

**Vantaggi**

* Accesso diretto a tempo costante

**Svantaggi**

Se il numero di vertici è pari a n, l'occupazione di memoria è sempre pari a teta di n^2 anche se non ci sono archi.

La matrice di adiacenza dovrà salvare comunque tutti zero.

**Come si può ovviare?**

**Se il grafo è non orientato** (gli archi non hanno senso) la matrice di adiacenza è simmetrica rispetto alla diagonale.

##### Lista di adiacenza

Creo n liste, una per ogni vertice,

in pratica un array di liste, dove ogni lista avrà come testa i vertici e sarà costituita da tutti gli elementi con cui il vertice è associato tramite archi (l'ordine non ha importanza)

La struttura di una lista di adiacenza è molto simile alle hash map,

infatti è possibile usare una hashmap con chaining per rappresentare una lista di adiacenza.

**Vantaggi**

* Richiede memoria massima O grande di (|V|+|E|)
* inserimenti e cancellazione veloci.

**Svantaggi**

* Accesso sequenziale ( a differenza del diretto, in cui per accedere al dato posso farlo direttamente accedendo alla cella di memoria che lo contiene, per accedere al dato nell' accesso sequenziale devo scorrere la lista, nel caso peggiore dovrò scorrerla completamente, tempo lineare sul numero di elementi della lista, in questo caso del numero di archi )

**Densità di un grafo**

Sia G=(V,E), con n=|V| ovvero sia n il numero di elementi dell’insieme dei vertici.

Densità di (G) = |E| / |V|^2

##### Visita di un grafo