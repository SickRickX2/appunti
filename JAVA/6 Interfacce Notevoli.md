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