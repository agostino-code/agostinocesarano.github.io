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

è possibile incrementare un puntatore costante e punterà alla cella di memoria successiva,ma non è possibile incrementare un valore costante.

Il valore di una costante deve essere sempre definito, non posso dichiarare una costante senza assegnare un valore.

##### Puntatori

Un puntatore e' un tipo di dato, una variabile che contiene l'indirizzo in memoria di un'altra variabile. Si possono avere puntatori a qualsiasi tipo di variabile.

**Dichiarazione puntatori**

```cpp
type* varname [ = riferimento indirizzo];
```

Ricordiamo che la dimenzione di un puntatore non dipende dal tipo di dato puntato, ma dal tipo di architettura della macchina in uso, genericamente 64 Bit nelle nuove macchine, 32 Bit nelle macchine obsolete.

*Esempi di utilizzo*

```cpp
char c='a';
char* p = &c ;
cout<< *p <<endl;
p = nullptr; //nullptr corrisponde alla NULL assegniata al puntatore in C.
cout<< c <<endl;
//Attenzione errori comuni!
cout<< *p <<endl; 
/* In questo caso avro un Segmentation fault,
non posso stampare un puntatore null */
cout<< p <<endl; 
/* In questo caso la stampa del valore non va
a buon fine, provato stampa simboli senza senso */
```

*Altri esempi di errore*

```cpp
const char c ='b'
char* p = &c; 
/* Errore,non posso assegnare l'indirizzo di una costante
ad un puntatore classico, potrei modificare una costante.
Questo porterebbe ad un errore.*/
const char* p = &c; //Modo corretto.
```

Posso fare il contrario, puntore costante ad una variabile, non permette la modifica dell'indirizzo del puntato. 

##### Puntatore Void

```cpp
void* varname [ = riferimento indirizzo];
```

*Esempi di utilizzo*

```cpp
void* p = &c;
/* Il puntatore void non fa la stampa,avremo un errore.
Quando dichiariamo il tipo di un puntatore definiamo già il tipo
che ci sarà in quella locazione di memoria è quindi stamperà il valore.*/
cout<< *((char *)p) <<endl;
cout<< *(static_cast <char *>(p)) <<endl; 
/* Possiamo fare il cast del tipo per permettere la stampa del valore.
Si preferisce il cast fatto nel secondo modo C++ Like*/
```

##### Riferimenti

Le variabili Reference accedono alla stessa locazione di memoria della  variabile che gli assegniamo,tutte le operazioni fatte sul riferimento si rifletteranno automaticamente sulla variabile a cui punta; e viceversa.

**Dichiarazione riferimenti**

```cpp
type& varname = variabile
```

*Esempi di utilizzo*

```cpp
int a = 0;
int& b = a;
  
int& c= 0; //Errato non posso associare una costante ad un riferimento non costante
const int& c = 0; //Corretto
  
int g = f();
b = g; //Errato non possiamo cambiare il riferimento dopo la dichiarazione!

int& r; //Errato una variabile reference deve essere inizializzata!

int& d = f(); //Non posso associare un valore di return di una funzione (temporaneo) ad un riferimento
```

##### New and Delete

Per quella che riguarda l'allocazione dinamica della memoria in C++ le strutture che permettono l'allocazione sono:

> ```cpp
> new
> delete
> ```

Le differenze principali tra *malloc in c* e *new in c++* sono:

Se la funzione malloc fallisce, ritorna con un puntatore NULL. L'operatore new non restituisce mai un puntatore NULL ma indica l'errore generando invece un'eccezione **bad_alloc.**

*Esempi di utilizzo*

```cpp
  try {

    ulong* ulptr = new ulong; //Unsigned long non inizialiozzato
    // ulong* ulptr = new ulong(5); // new ulong{5} //Unsigned long inizializzato a 5

    cout << (*ulptr)++ << endl;
    cout << *ulptr << endl;

    delete ulptr; // ulptr = nullptr;
    // delete ulptr; // La doppia delete viene ignorata

  } catch (bad_alloc exc) {
    cout << "Quite rare exception!" << endl;
  }
```

*Altro esempio di utilizzo*

```cpp
  try {

    const ulong arraysize = 3; // Se la dimenzione impostata e molto grande ci darà l'exception

    ulong* ulptr = new ulong[arraysize]; //Array non inizializzato di tre unsigned longs
    // ulong* ulptr = new ulong[arraysize]{}; //Array di tre unsigned long inizializzati a (0)
    // ulong* ulptr = new ulong[arraysize]{5, 6, 7}; //Array di tre unsigned long inizializzati a 5, 6, e 7.

    cout << ulptr[0]++ << endl;
    cout << ulptr[1] << endl;
    cout << ulptr[2]-- << endl << endl;

    cout << ulptr[0] << endl;
    cout << ulptr[1] << endl;
    cout << ulptr[2] << endl;

    delete[] ulptr; // ulptr = nullptr;
    // delete[] ulptr; // La doppia delete viene ignorata

  } catch (bad_alloc exc) {
    cout << "Quite rare exception!" << endl;
  }
```

A differenza di Java,dove la gestione della memoria è affidata al Garbage Collector, la gestione in C++ è a carico del progammatore, si deve eliminare tutto ciò che non usiamo manualmente con delle delete.

Nelle allocazioni all'interno di costruttori in genere non ci vuole il try catch.

##### Struct

**Dichiarazione struct**

```cpp
struct StructName{
  campi
}

StructName={campo,...,campo}
```

**Accesso alle Struct**

```cpp
//Member access
StructName.campo;

//Accesso via puntatore
(*PointerName).campo;
PointerName -> campo;
```

Le Struct in C++ sono delle vere e proprie classi,nelle struct gli attributi sono tutti di tipo pubblico.

Posso definire anche definire attributi Privati

```cpp
struct StructName{
//public:
  campi
    
private:
  campi
}
//L'accesso a questi campi è possibile sono le funzione è amica
friend
```

**Enumerazioni**

**Dichiarazione enum**

```cpp
enum class enumName{elemento,...,elemento};
enum enumName{...};/* C Like,gli elementi sono globali,
non posso dichiarare un altro elemento con lo stesso nome in un altra enum,
sarebbe un errore,ecco perchè è preferibile usare il primo modo di C++ */
```

**Accesso ai valori di un enum**

```cpp
enumName::elemento
```

Le enumerazioni possono essere confrontate: ==,!=,<,>,<=,>= 

o assegnate: =

Levariabili di tipo enumerativo possono ovviamanete abvere un valore di default iniziale.

##### Libreria <iostream>

**Dichiarazione libreria**

```cpp
#include<iostream>
```

**Operatori principali**

```cpp
<< //put-to
>> //get-from
```

**Standard Stream**

```cpp
cerr //
cout //Output stream : ostream
clog //
  
cin //Input stream : istream
```

**Override degli operatori di put-to e get-from**

*Esempio di utilizzo*

```cpp
struct Studente {

  ulong Id = 0;
  string Matricola = "N86000000";
  string Cognome = "";
  string Nome = "";

   friend ostream& operator<<(ostream& outstr, const Studente& stu); 
  //Dichiaro la funzione amica,può accede agli attributi privati per l'output

   friend istream& operator>>(istream& instr, Studente& stu);
  //Dichiaro la funzione amica,può accede agli attributi privati per l'input
  
   private:

   ulong SecureNum = 0x25242310; //Attributo privato

};

ostream& operator<<(ostream& outstr, const Studente& stu) { 
  // Definisco l'output della struct Studente
  outstr << "Id: " << stu.Id << "; Matricola: " << stu.Matricola 
    << "; Cognome: " << stu.Cognome << "; Nome: " << stu.Nome;
  outstr << "; Numero di sicurezza: " << stu.SecureNum;
  return outstr;
}

istream& operator>>(istream& instr, Studente& stu) {
  //Definisco l'input della struct Studente
  instr >> stu.Id >> stu.Matricola >> stu.Cognome >> stu.Nome;
  instr >> stu.SecureNum;
  return instr;
}

enum class Color { Giallo, Verde, Bianco, Rosso };

ostream& operator<<(ostream& outstr, const Color& clr) {
  switch(clr) {
    case Color::Verde:
      outstr << "Green";
      break;
    case Color::Bianco:
      outstr << "White";
      break;
    case Color::Rosso:
      outstr << "Red";
      break;
    default:
      outstr << "Color{ " << int(clr) << " }";
  }
  return outstr;
}
```

**Funzioni di libreria**

```cpp
//Classe istream
good(); eof(); fail(); bad(); //Funzioni per l'analisi dello Stato
get(c); getline(p,n) //c char, p puntatore char, numero di caratteri da leggere
  
//Classe ostream
put(c); write(p,n) //c char, p puntatore const char, numero di caratteri da leggere
```

##### Libreria <string>

**Dichiarazione libreria**

```cpp
#include<string>
```

Libreria che introduce l'oggetto stringa, non è un array di char.

**Dichiarazione di stringhe**

```cpp
String VarName="alone";
String VarName={"alone"};
String VarName("alone");
```

Gli oggetti stringa sono confrontabili logicamente ==,!=,<=,>=,<,>.

Gli operatori di put-to e get-from tramite *override* permettono output e input degli oggetti di tipo stringa.

**Funzioni di libreria**

```cpp
size(); //Restituisce la size della stringa.
empty(); //Restituisce un booleano,true se la stringa è vuota.
[i]; //Permette di accedere all' i-esimo carattere.
front() //Restituisce il primo carattere della stringa.
back() //Restituisce l'ultimo carattere della stringa.
```

**Concatenazione di tipi stringa**

La concatenazione tra oggetti di tipi stringa, viene effettuata tramite l'operatore "+".

```cpp
String var= var1+ var2 //Il valore della concatenazione viene inserito nella variabiloe var.
String var+= var1 //Il valore della concatenazione viene inserito direttamente nella variabile più a sinistra.  
```

**Sottostringhe**

```cpp
String var;
var.substr(i,n) //Testituisce la sottostringa da posizione i a posizione i+n-1
```

##### Classi

**Dichiarazione delle classi**

```cpp
  class ClassName{
  private:
    //Attributi e funzioni privati, ossia accessibili solo all'interno della classe
  protected:
    //Attributi e metodi visibili solo con altre classi nella gerarchia.
  public:
    //Attributi e motodi visibili a tutti.   
} 
```

**Costruttori**

```cpp
ClassName(); //Default costructor
ClassName(parametri); //Specific constructor
ClassName(const ClassName&); //Copy constructor
ClassNAme(ClassName&&) noexept; //Move constructor
```

**Distruttore**

```cpp
~ClassName(); //Distruttore
```

**Attenzione!** Non ci sarà mai bisogno di chiamare un distruttore nelle librerie che creeremo.

*Ereditarietà delle classi in C++*

La differenza principale rispetto a JAVA è che in C++ non esistono le *Interface*, infatti è il programmatore che deve distinguere se quella classe è un **Interfaccia** o un **estensione**.

**Dichiarazione di classi estensione**

```cpp
class ClassName : [virtual][private/protected/public] BaseClassName,...{
...
} //Private è il metodo di default
```