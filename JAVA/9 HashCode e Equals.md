I metodi *equals()* e *hashcode()* sono metodi importanti in java che ogni oggetto eredita dalla classe Object

## Equals
Il metodo *equals()* viene utilizzato per verificare se due oggetti sono uguali:
>[!tip] Implementazione di base in Object
>Nella sua implementazione  di base in Object il metodo controlla se i due oggetti si riferiscono alla stessa area di memoria ovvero se sono lo stesso oggetto

### Override
Se *equals* viene sovrascritto allora dobbiamo ri-implementare anche *hashCode()*.

Per sovrascrivere *equals()* in modo tale che due oggetti siano logicamente uguali bisogna:
1) **Verificare se l'oggetto è null**: il primo passo è verificare se l'oggetto passato come parametro è null. Se null restituisce false
2) **Verificare se l'oggetto è dello stesso tipo**: il secondo passo è verificare se l'oggetto passato come parametro  è dello stesso tipo della classe in cui  si sta scrivendo il metodo
3) **Confrontare le proprietà**: il terzo passo è confrontare le proprietà dell'oggetto passato come parametro con le proprietà dell'oggetto corrente
4) **Restituire il risultato**

## HashCode
*hashCode()* è un metodo di *object* che associa ad ogni oggetto un codice hash (ovvero un numreo intero) che sarà lo stesso per due oggetti uguali.

Il metodo *hashcode* è utilizzato nelle strutture dati *HashMap* e *HashSet*, che utilizzando il codice di hash per organizzare gli oggetti.
**Osservazione**: Se due oggetti sono uguali secondo equals() allora dovranno avere lo stesso hash code, tuttavia se due oggetti hanno lo stesso hash code non implica che siano necessariamente uguali secondo il metodo equals()

### Override
Se equals viene sovrascritto allor dobbiamo ri-implementare anche hashCode.
1) **Numeri Primi**: Scegliamo 2 numeri primi uno è utilizzato per inizializzare  il codice hash, l'altro per moltiplicare i valore dei campi
2) **Hash dei campi**: si deve calcolare il codice hash di ogni campo dell'oggetto, i primitivi si sommano direttamente mentre gli altri tipi si sommano usando il metodo hashCode()
3) **Somme e Prodotto**: 
	-  si inizializza il valore dell'hash con il primo numero prim che si è scelto
	- per ogni campo dell'oggetto: si moltiplica il valore dell'hash con il secondo numero primo poi sommiamo al nuovo hash l'hash code del campo che si sta prendendo in considerazione