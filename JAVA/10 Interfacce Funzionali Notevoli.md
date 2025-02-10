## Function
L'interfaccia funzionale *Function<T, R>* in Java è un'interfaccia fuznionale che rappresenta una funzione che accetta un argomento di tipo *T* e restituisce un valore di tipo *R*.
 Contiene un metodo **apply**: *R apply(T t)*

## Predicate
L'interfaccia funzionale *Predicate<T,>* in Java rappresenta una funzione che accetta un argomento di tipo T e restituisce u valore booleano.
Contiene il metodo **test**: *boolean test(T t)*

## Supplier
L'interfaccia *Supplier<T.>* in Java rappresenta una funzione che non accetta argomenti e restituisce un valore di tipo *<T.>*

## Consumer 
L'interfaccia funzionale *Consumer<T.>* in Java rappresenta una funzione che accetta un argomento di tipo T e non restituisce alcun valore
L'interfaccia `Consumer` ha un solo metodo astratto, chiamato `accept`, che viene utilizzato per eseguire l'azione sulla classe di tipo `T`.
