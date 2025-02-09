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

Il metodo *hashcode* è utilizzato nelle strutture dati *HashMap* e *HashSet* 