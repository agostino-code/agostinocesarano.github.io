---
title: Laboratorio Algoritmi e Strutture Dati (Esercizio 4)
date: 2022-06-21T11:29:41.195Z
author: Agostino Cesarano
summary: Appunti per il corso di LASD, Professore Mogavero; esercizio numero 4,
  alberi binari di ricerca.
tags:
  - LASD
---
##### BST

Il BST è un albero binario che rispetta tre proprietà:

1. Il sottoalbero sinistro di un nodo x contiene soltanto i nodi con chiavi minori della chiave del nodo x,
2. Il sottoalbero destro di un nodo x contiene soltanto i nodi con chiavi maggiori della chiave del nodo x,
3. Il sottoalbero destro e il sottoalbero sinistro devono essere entrambi due alberi binari di ricerca;

**Implementazione in C++ personale**

**Funzioni ausiliarie**

```cpp
  void DeleteNode(NodeLnk*&,const Data&);
  Data DataNDelete(NodeLnk*);

  NodeLnk* Detach(NodeLnk*&) noexcept;

  NodeLnk* DetachMin(NodeLnk*&) noexcept;
  NodeLnk* DetachMax(NodeLnk*&) noexcept;

  NodeLnk* Skip2Left(NodeLnk*&) noexcept;
  NodeLnk* Skip2Right(NodeLnk*&) noexcept;

  NodeLnk* const& FindPointerToMin(NodeLnk* const &) const noexcept; // Both mutable & unmutable versions
  NodeLnk*& FindPointerToMin(NodeLnk*&) noexcept; // Both mutable & unmutable versions

  NodeLnk* const& FindPointerToMax(NodeLnk* const &) const noexcept; // Both mutable & unmutable versions
  NodeLnk*& FindPointerToMax(NodeLnk*&) noexcept; // Both mutable & unmutable versions

  NodeLnk* const & FindPointerTo(NodeLnk* const &,const Data&) const noexcept; // Both mutable & unmutable versions
  NodeLnk*& FindPointerTo(NodeLnk*&,const Data&) noexcept; // Both mutable & unmutable versions

  NodeLnk* const* FindPointerToPredecessor(NodeLnk* const&,const Data&) const noexcept; // Both mutable & unmutable versions
  NodeLnk** FindPointerToPredecessor(NodeLnk*&,const Data&)noexcept; // Both mutable & unmutable versions

  NodeLnk* const* FindPointerToSuccessor(NodeLnk* const&,const Data&) const noexcept; // Both mutable & unmutable versions
  NodeLnk** FindPointerToSuccessor(NodeLnk*&,const Data&)noexcept; // Both mutable & unmutable versions
```

**DeleteNode**

Ha come parametri il nodo, che sarà la radice dell'albero di cui vogliamo eliminare il nodo, e la chiave da eliminare nell'albero.

L'algoritmo tramite ricerca binaria trova il nodo con la chiave da eliminare e in base a quelle che saranno le condizioni di quel nodo:

1. Se il nodo è una foglia, elimino il nodo,
2. Se il nodo ha figlio destro e figlio sinistro, sostituisci il nodo  da cancellare con il max del sottoalbero sinistro,
3. Se il nodo ha figlio destro o figlio sinistro, sostituisco il nodo da cancellare con il nodo figlio.

**DataNDelete**

Elimino il nodo e restituisco il dato.

**Detach**

Stacca il nodo e restituisce un puntatore al nodo.

**DetachMin**

Prende il minimo e lo stacca, ne restituisce un puntatore. Usa la funzione ausiliaria *SkipToLeft.*

**DetachMax**

Prende il massimo e lo stacca, ne restituisce un puntatore. Usa la funzione ausiliaria *SkipToRight.*

**SkipToLeft**

Prende il nodo sinistro e lo sostituisce al nodo attuale.

**SkipToRight**

Prende il nodo destro e lo sostituisce al nodo attuale.

**FindPointer**

Discesa tramite ricerca binaria, in base ai contesti cambia l'algoritmo.

Se devo cercare il massimo, andrò a visitare il sottoalbero destro di quel nodo.

Se devo cercare il minimo, andrò a visitare il sottoalbero destro di quel nodo.