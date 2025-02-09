*Clone()* è un metodo che ogni classe eredita dalla superclasse *object* e restituisce una copia dell'oggetto clonato (ovvero una nuova istanza dell'oggetto con stessi campi ma area di memoria diversa).

Normalmente non è possibile chiamare il metodo, per fare ciò dobbiamo usare l'interfaccia **segnaposto** *cloneable*, e poi effettuare un override e fornire un implementazione del metodo *clone()*.
Interfaccia Segnaposto
>[!warning] Interfaccia Segnaposto
L'interfaccia `cloneable` è detta interfaccia segna posto perché non contiene nessun metodo, infatti è semplicemente utilizzata per segnalare alla Java Virtual Machine che l’oggetto può essere clonato

## Clone Shallow Copy
Per fare una shallow copy bisogna semplicemente chiamare il metodo clone() della superclasse (object).

La shallow copy consiste in un nuovo oggetto in cui:
- i campi primitivi saranno copiati e avranno valori identici all'oggetto originale
- i riferimenti agli oggetti saranno copiati  ma punteranno alla stessa area di memoria dell'oggetto originale
## Clone Deep Copy
Il metodo più complesso per effettuare un clone è creare una copia in cui ogni riferimento ad un altro oggetto dovrà implementare *cloneable*

La deep copy consiste in:
- I campi primitivi saranno copiati e avranno valor