Il polimorfismo è un concetto fondamentale nella programmazione orientata ad oggetti.
In generale, si riferisce alla capacità di assumere diverse forme o comportamenti a seconda del contesto in cui viene utilizzato.
Più nello specifico permette di utilizzare lo stess ocodice su oggetti diversi, ma che condividono una classe madre. Ciò significa che possiamo creare codice che funziona con oggetti di tipo diverso (ma che ereditano la stessa classe), senza dover scrivere codice specifico perr ogni tipo di oggetto.

## Binding
Il binding è il processo che determina quale oggetto deve essere utilizzato quando si chiama un metodo o si accede a una variabile.

Infatti per la presenza di polimorfismo, il tipo di riferimento (variabile) può non corrispondere al tipo dell'oggetto vero e proprio presente in memoria.

>[!note] Binding Statico
>Il **Binding Statico** o early binding, si verifica quando il tipo di un oggetto o di un metodo viene determinato durante la *compilazione* del codice.
>Si utilizza per tutti quei metodi che non possono essere sovrascritti dalle sottoclassi ovvero metodi:
>- *statici*
>- *final*
>- *private*

>[!note] Binding Dinamico
>**Binding Dinamico** o late binding, si verifica quando il tipo di un oggetto o di un metodo viene determinato durante *l'esecuzione* del codice.
>Il metodo effettivo viene determinato a runtime in base al tipo concreto dell'oggetto e non al tipo della variabile di riferimento.
>Ad esempio:
>```Java
>Animal animale = new Cane(); animale.abbaia();
>```
>
> In questo caso il compilatore non può determinare con certezza quale metodo abbaia verrà chiamato, perché il tipo della variabile animale è Animal, ma l'oggetto vero e proprio è di tipo Cane. A runtime, il sistema verifica il tipo dell'oggetto e chiama il metodo.


