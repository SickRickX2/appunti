>[!note] # Final
>- **Classi**: le classi final non posssono essere estese. Nessuna classe può ereditare una classe final, impedisce che una classe venga modificata tramite l'ereditarietà
>- **Metodi**: Un metodo dichiarato final non può essere sovrascritto tramite @override da nessuna sottoclasse
>- **Campi**: i campi final non posssono essere modificati dopo la loro assegnazione

>[!tip] # Static
>- **Classi**: non è possibile definire static una classe standard ma sono su una classe dichiarata all'interno di un'altra classe.
>	Un'*inner class*(non statica) non può essere istanziata senza creare un'istanza della sua classe esterna e  ha accesso ai campi e metodi della classe esterna.
>	 Una *nested class* (statica) può essere istanziata senza istanziare la sua classe esterna e ha accesso solo ai membri statici della classe esterna
>- **Metodi**: i metodi statici appartengono alla classe e  non ad un'istanza specifica e possono solo utilizzare metodi e campi statici
>- **Campi**: appartengono ad una classe e non ad un istanza precisa  quindi esiste una sola allocazione del dato che è condivisa tra tutte le istanze

>[!Example] # Abstract
>Può essere usata solo su metodi e classi:
>- **Classi**: le classi astratte non possono essere istanziate ma solo estese, può contenere metodi astratti o non
>- **Metodi**:i metodi astratti non forniscono un'implementazione, ma le sottoclassi non astratte sono obbligate a fornirla rispettando il nome del metodo, i parametri in in input e il tipo di ritorno

