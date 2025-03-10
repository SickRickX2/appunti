## Iterable e Iterator
In Java, le interfacce *Iterable* e *Iterator* sono due concetti fondamentali per lavorare con collezione di dati.
>[!note] Iterable
>L'interfaccia *Iterable* rappresenta una collezione di oggetti che può essere iterata, ovvero può essere scorsa elemento per elemento. Una classe che implementa *Iterable* deve fornire un metodo *Iterator()* che restituisce un oggetto *Iterator* che può essere utilizzato per scorrere la collezione

>[!tip] Iterator
>L'interfaccia *Iterator* rappresenta un oggetto che può essere utilizzato per scorrere una collezione di oggetti, che deve fornire tre metodi:
>- *hasNext()*: restituisce *true* se ci sono ancora elementi da scorrere, *false* altrimenti
>- *next()*: restituisce l'elemento successivo nella collezione
>- *remove()*: rimuove l'elemento corrente dalla collezione (non è obbligatorio implementare questo metodo)

## List Iterator
*ListIterator* è un interfaccia che estende l'interfaccia *Iterator* ed è specifica per liste. E implementa questi metodi:
- `hasNext()`: restituisce `true` se ci sono ancora elementi da scorrere in avanti, `false` altrimenti.
- `hasPrevious()`: restituisce `true` se ci sono ancora elementi da scorrere all'indietro, `false` altrimenti.
- `next()`: restituisce l'elemento successivo nella lista.
- `previous()`: restituisce l'elemento precedente nella lista.
- `remove()`: rimuove l'elemento corrente dalla lista.
- `set(Object o)`: sostituisce l'elemento corrente con l'oggetto specificato.
- `add(Object o)`: aggiunge l'oggetto specificato alla lista.

## Comparable
*Comparable* è un'interfaccia funzionale che consente di definire un ordinamento per una classe  di oggetti.
Una classe che implementa *Comparable* deve fornire un metodo *compareTo()* che confronta l'oggetto da cui è chiamato con altro oggetto della stessa classe e restituisce:
- 0 se sono uguali
- 1 se il primo è maggiore
- -1 se il primo è minore
## Comparator
*Comparator* è un'interfaccia funzionale che consente di definire un ordinamento personalizzato per una classe di oggetti.

Una classe che implementa *Comparator* deve fornire un metodo *compare()* che confronta due oggetti della stessa classe e restituisce un valore intero che indica l'ordinamento tra i due oggetti.
**Differenze:**
- *Comparable* è un'interfaccia che deve essere implementata dalla classe stessa, mentre *Comparator* può essere implementata da una classe esterna.
- *Comparable* definisce un ordinamento naturale per la classe , mentre *Comparator* definisce un ordinamento personalizzato
## Cloneable
Cloneable è un'interfaccia segnaposto di Clone
## Serializable
L'interfaccia Serializable in Java è un'interfaccia segna posto (cioè non contiene metodi) che indica che un oggetto può essere serializzato, ovvero convertito in un flusso di byte che può essere scritto su un file o inviato su una rete.




