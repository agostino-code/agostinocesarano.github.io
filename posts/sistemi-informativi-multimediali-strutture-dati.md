---
title: Sistemi Informativi Multimediali (Strutture dati)
date: 2022-06-17T01:47:34.638Z
author: Agostino Cesarano
summary: Appunti per il corso di SIM, Professore Balzano; quarta parte,
  strutture dati per l'archiviazione dei media e feature vector.
tags:
  - SIM
---
##### Tecniche e strutture dati per la ricerca efficiente di similarità nei dati multimediali

Le feature, una volta estratte, vengono rappresentate attraverso vettori multidimensionali:

Zero crossing rate, Silence ratio, Istogrammi di colore.. ecc.

Le caratteristiche devono caratterizzare in modo univoco l’oggetto (non estremamente tante!)

La similarità o la distanza sono calcolate come distanza tra i vettori che rappresentano le feature estratte.

Il calcolo della similarità è un’operazione computazionalmente dispendiosa.

Se la dimensionalità del vettore è grande, i tempi di ricerca per confrontare tutti i vettori dei dati
memorizzati con la query diventano troppo lunghi!


Occorrono tecniche e strutture dati che permettano di organizzare i vettori multidimensionali e di
effettuare le ricerche in modo veloce.


**Tipi di query e vettori**

Quando facciamo un confronto tra query input e oggetti memorizzati nel database, per il recupero del risultato in modo efficiente cerchiamo di minimizzare il numero dei confronti.

La query è rappresentata dal vettore rosso.

Il risultato che cerchiamo è rappresentato dal vettore verde.

**POINT QUERY**

Una query utente è rappresentata da un vettore e la ricerca ha come obiettivo quello di trovare gli oggetti memorizzati nel database il cui vettore delle feature risulta identico a quello della query **(exact match)**

![Point query](/static/img/point-query.jpg "Point query")

**RANGE QUERY**

La query è rappresentata da un vettore e da un range di distanza. Tutti gli oggetti la cui distanza dalla query è inferiore o uguale a quella specificata sono ritrovati.

![Range query](/static/img/range-query.jpg "Range query")

*Se diamo raggio r = 0 diventa una point query. Raggio enorme: poco
efficiente. L’intorno deve essere ragionevolmente piccolo.*

*Sia dato un punto, si definisce intorno di un punto un insieme la cui distanza tra i punti appartenenti all’insieme sia inferiore o uguale al raggio r.*

**K‐NEAREST NEIGHBOR**

Se non trova risultati per la query anche entro un certo raggio,
esce fuori al raggio e cerca le k risposte più vicine alla query in input, le quali possono anche **non
essere** attinenti alla query in input.

![K-nearest query](/static/img/k-nearest-query.jpg "k-nearest query")