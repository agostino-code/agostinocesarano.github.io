---
title: Sistemi Informativi Multimediali (MIRS)
date: 2022-05-24T08:21:00.876Z
author: Agostino Cesarano
summary: Appunti per il corso di SIM, Professore Balzano; seconda parte, i MIRS.
tags:
  - SIM
---
##### Architettura dei MIRS

![Architettura di un MIRS](/static/img/architettura-mirs.png "Architettura di un MIRS")

La prima fase è quella di inserimento nel MIRS.

**Fase 1 (Inserimento)**

1. L'Utente specifica un tipo di Input ( microfono, CD, videocamera ).
2. I contenuti vengono estratti dal database automaticamente o semi-automaticamente.
3. Gli oggetti vengono inviati al server, con le relative caratteristiche.
4. Gli oggetti in arrivo vengono organizzati e spediti al prossimo blocco.
5. Esegue l'indicizzazione delle informazione.
6. Memorizza le informazioni indicizzate e gli oggetti.

La seconda fase è quella del recupero delle informazione, il modello è lo stesso cambia il tipo di operazioni effettuate.

**Fase 2 (Recupero)**

1. L'Utente esegue una Query sul database, l'oggetto ricercato può anche non essere presente.
2. Vengono analizzata la Query.
3. Il Client raccoglie i dati che la query richiede.
4. Il Server riceve i dati e li smista alla indicizzazione.
5. Il motore di indicizzazione reperisce gli elementi nel database più pertinenti alla ricerca.
6. Recupero dell'oggetto richiesto ed invio all'interfaccia utente.