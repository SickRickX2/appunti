*Clone()* è un metodo che ogni classe eredita dalla superclasse *object* e restituisce una copia dell'oggetto clonato (ovvero una nuova istanza dell'oggetto con stessi campi ma area di memoria diversa).

Normalmente non è possibile chiamare il metodo, per fare ciò dobbiamo usare l'interfaccia **segnaposto** *cloneable*, e poi effettuare un override e fornire un implementazione del metodo *clone()*.
Interfaccia Segnaposto
>[!warning] Interfaccia Segnaposto
L'interfaccia `cloneable` è detta interfaccia segna posto perché non contiene nessun metodo, infatti è semplicemente utilizzata per segnalare alla Java Virtual Machine che l’oggetto può essere clonato

## Clone Shallow Copy
Per fare una shallow copy bisogna semplicemente chiamare il metodo clone() della superclasse (object).

