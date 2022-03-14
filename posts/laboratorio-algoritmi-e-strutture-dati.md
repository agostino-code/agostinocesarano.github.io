---
title: Laboratorio Algoritmi e Strutture Dati
date: 2022-03-14T10:42:54.368Z
author: Agostino Cesarano
summary: Appunti per il corso di LASD, Professore Mogavero.
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
> ```cpp
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

```cpp
const type varname = value;
```

##### Puntatori

**Dichiarazione puntatori**

```cpp
type* varname [ = riferimento indirizzo];
```

Ricordiamo che la dimenzione di un puntatore non dipende dal tipo di dato puntato, ma dal tipo di architettura della macchina in uso, genericamente 64 Bit nelle nuove macchine, 32 Bit nelle macchine obsolete.

*Esempi di utilizzo*

```cpp
char c='a';
char *p = &c ;
cout<< *p <<endl;
p = nullptr; //nullptr corrisponde alla NULL assegniata al puntatore in C.
cout<< c <<endl;
//Attenzione errori comuni!
cout<< *p <<endl; 
/* In questo caso avro un Segmentation fault,
non posso stampare un puntatore null */
cout<< p <<endl; 
/* In questo caso la stampa del valore
non va a buon fine, provato stampa simboli senza senso */
```

*Altri esempi di errore*

```cpp
const char c ='b'
char *p = &c; 
/* Errore,non posso assegnare l'indirizzo di una costante
ad un puntatore classico, potrei modificare una costante.
Questo porterebbe ad un errore.*/
const char *p = &c; //Modo corretto.
```

Posso fare il contrario, puntore costante ad una variabile, non permette la modifica dell'indirizzo del puntato. 

##### Puntatore Void