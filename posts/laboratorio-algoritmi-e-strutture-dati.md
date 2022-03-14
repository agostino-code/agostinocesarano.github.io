---
title: Laboratorio Algoritmi e Strutture Dati
date: 2022-03-14T10:42:54.368Z
author: Agostino Cesarano
summary: Appunti LASD
metaDescription: ""
tags:
  - LASD
---
Il linguaggio di progammazione usato in questo corso è il C++ che a livello di sintassi non differisce molto dal C , ma ha alcune pecularità che gli danno una propria identità.

##### Tipi fondamentali in C++

**Dichiarazione variabili**

```cpp
type varname [ =default value ];
type varname[n] [ ={ val0,...,valn} ];
```

* *bool* non presente nativamente in C ma presente nelle librerie standard di C++
* unsigned anche questo non presente in C ma presente in C++

A differenza degli int e long, che utilizzano un bit per la rappresentazione del segno, unsigned usa tutti i *2^n Bit* per la rappresentazione dei numeri Naturali.

> In base al compilatore sono presenti sono presenti u***type***/unsigned ***type***
>
> ```
> unsigned type varname [ =default value ];
> ```

*Dove per type si intente uno dei tipi fondamentali riportati in seguito :*

* char
* short
* int
* long int
* long long int
* float
* double
* long double

L'ultimo non per importanza è il tipo const che permette di definire costanti, valori di sola lettura. Utili anche nel passaggio dei puntatori nelle chiamate a funzione.

```
const type varname = value;
```

##### Puntatori

**Dichiarazione puntatori**

```
type
```