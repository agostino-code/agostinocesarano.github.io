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

**Matrice di adiacenza**

Creo una matrice i x j, ogni cella rappresenta una coppia di vertici M(Vi,Vj).

Ogni cella avrà valore 1 se la coppia di vertici è associata con un arco, quindi la coppia appartiene all'insieme E.

Altrimenti avrà valore 0.

**Lista di adiacenza**

Creo n liste, una per ogni vertice,

in pratica un array di liste, dove ogni lista avrà come testa i vertici e sarà costituita da tutti gli elementi con cui il vertice è associato tramite archi (l'ordine non ha importanza)