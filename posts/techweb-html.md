---
title: TechWeb (HTML)
date: 2023-10-21T10:38:40.686Z
author: Agostino Cesarano
summary: Appunti per il corso di TechWeb, Professoressa Anna Corazza, HTML.
tags:
  - TechWeb
---
# HTML

HTML (HyperText Markup Language) è il linguaggio di markup utilizzato per creare e strutturare le pagine web.

Viene utilizzato per definire la struttura logica e il contenuto di una pagina web, come titoli, paragrafi, immagini, collegamenti ipertestuali e altro ancora. HTML è uno dei pilastri fondamentali della creazione di pagine web ed è supportato da tutti i browser moderni.

Le pagine HTML sono composte da elementi HTML, ciascuno identificato da tag circondati da parentesi angolari. Ad esempio, il tag per creare un paragrafo è `<p>`, mentre il tag per inserire un'immagine è `<img>`. Ogni elemento può contenere testo e/o altri elementi nidificati.

Ecco un esempio semplice di una pagina HTML:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Titolo della pagina</title>
</head>
<body>
    <h1>Benvenuti nella mia pagina web</h1>
    <p>Questa è una semplice pagina HTML.</p>
    <img src="immagine.jpg" alt="Descrizione dell'immagine">
    <a href="<https://www.esempio.com>">Visita il nostro sito web</a>
</body>
</html>
```

In questo esempio, abbiamo una pagina HTML con un titolo (`<title>`), un'intestazione di livello 1 (`<h1>`), un paragrafo (`<p>`), un'immagine (`<img>`), e un collegamento ipertestuale (`<a>`) che porta a un altro sito web.

Il browser interpreta il codice HTML e visualizza la pagina web in base alla struttura e al contenuto definiti dagli elementi HTML.

> Oltre ad HTML, le pagine web sono spesso accompagnate da fogli di stile CSS (Cascading Style Sheets) per definire l'aspetto visivo della pagina e da script JavaScript per aggiungere funzionalità interattive.

Insieme, HTML, CSS e JavaScript costituiscono la base della maggior parte dei siti web moderni.

- - -

HTML, però oltre alle indicazioni sulla struttura del documento, prevede anche delle etichette per interagire con l’utente. Infatti, l’utente può dare origine a degli eventi a cui verranno associate diverse azioni.

Esempi di questo tipo di etichette sono quelle per la costruzione di moduli o form
per la raccolta dati e di bottoni per la creazione di una richiesta HTTP da inoltrare.

Le form rappresentano uno, ma non l’unico, dei modi per passare parametri al server.

```html
<form action="http://somesite.com/prog/adduser" method="post">
    <p>
        <label for="firstname">First name:</label>
        <input type="text" id="firstname"><br>
        <label for="lastname">Last name:</label>
        <input type="text" id="lastname"><br>
        <label for="email">Email:</label>
        <input type="text" id="email"><br>
        <input type="radio" name="sex" value="Male"> Male<br>
        <input type="radio" name="sex" value="Female"> Female<br>
        <input type="submit" value="Send"> 
        <input type="reset">
    </p>
```

Normalmente la presenza di una form in un documento HTML presentato lato client implica programmazione lato server per implementare un programma che prenda in ingresso i parametri raccolti dalla form e li elabori in modo opportuno.


💡 **ATTENZIONE** Non bisogna confondere il c**oncetto di elemento con quello di etichetta**. Infatti, **l’elemento è una parte di documento, mentre l’etichetta è semplicemente un nome, che in un certo senso caratterizza il tipo dell’elemento** (ad esempio, se si tratta di un titolo o di un paragrafo). In un documento possono esserci più elementi con la stessa etichetta. La stessa considerazione ovviamente vale anche per l’XML.

### HTML5

HTML5 è stato adottato principalmente per rispondere alle esigenze di sviluppo web moderne e per migliorare l'esperienza dell'utente sul web.

Alcune delle principali ragioni per l'adozione di HTML5 e le sue principali differenze rispetto alle versioni precedenti di HTML (come HTML 4) includono:

1. Supporto multimediale migliorato: HTML5 ha introdotto elementi nativi per l'inclusione di contenuti multimediali come audio e video **senza la necessità di plugin esterni come Adobe Flash.**
2. Elementi semantici: HTML5 ha introdotto nuovi **elementi semantici** come **`<header>`**, **`<nav>`**, **`<article>`**, **`<section>`**, **`<footer>`** e altri, **che rendono il codice HTML più chiaro** per i motori di ricerca e migliorano l'accessibilità.
3. Supporto per dispositivi mobili: HTML5 è stato progettato per essere più adatto per i dispositivi mobili, consentendo la creazione di siti web e **applicazioni web responsive che si adattano a diverse dimensioni di schermo e dispositivi**.
4. Miglioramenti nella gestione degli errori
5. **Supporto per le tecnologie moderne**: HTML5 è stato progettato per lavorare in sinergia con tecnologie moderne come **CSS e JavaScript.**
6. **Memorizzazione (storage):**
   Un’importante caratteristica di HTML5 riguarda la possibilità di memorizzare dati localmente, all’interno del browser, in alternativa ai cookies, sempre come coppia di stringhe nome-valore.

## Same Origin Policy

La Same-Origin Policy (SOP) o "Politica della Stessa Origine" **è un importante principio di sicurezza implementato dai browser web per proteggere gli utenti da potenziali minacce legate alla condivisione di risorse tra pagine web provenienti da diverse origini**. L'obiettivo principale della SOP è impedire che uno script in esecuzione su una pagina web di un'origine possa accedere o manipolare risorse di un'altra origine senza autorizzazione.

Un'origine in questo contesto è definita dalla combinazione di tre componenti:

1. Protocollo: Il protocollo utilizzato per accedere alla pagina, come HTTP o HTTPS.
2. Dominio: Il nome di dominio del sito web, come "[esempio.com](http://esempio.com/)".
3. Porta: Il numero di porta utilizzato nella richiesta, se specificato.

Anche detto **URI,** due URI sono considerate appartenere alla stessa origine se hanno uguali protocollo, dominio e porta.
Ad esempio, le seguenti risorse hanno tutte la stessa origine:[](http://example.com/)

<http://example.com/>

[http://example.com:80/](http://example.com/)

<http://example.com/path/file>

visto che la porta 80 è quella di default per il protocollo HTTP.

Le seguenti, invece, hanno origini
diverse:

<http://example.com:8080/>

<http://www.example.com/>

<https://example.com:80/>

[https://example.com](https://example.com/)/

<http://example.org/>

<http://ietf.org/>

> Tutte le risorse (ad esempio, script, stili, immagini, dati) caricate da questa pagina devono provenire dalla stessa origine per evitare problemi di sicurezza.


💡 La Same-Origin Policy è una misura di sicurezza importante che garantisce che le risorse di una pagina web siano isolate da altre origini, contribuendo a proteggere gli utenti da potenziali minacce e vulnerabilità.