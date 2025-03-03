Una *classe* è quel pezzo di codice che **descrive** i campi ed i metodi di un oggetto, viene definita dal programmatore, un *oggetto* quindi altro non è che un'**istanza** di una classe. In Java esistono delle classi già implementate in delle librerie, si possono trovare anche online scritte da altri programmatori. Queste sono organizzate in **package**.

## Campi e metodi
I campi costituiscono la memoria di un oggetto, sono delle variabili e hanno quindi un tipo e un nome. Di solito si definiscono privati all'interno della classe. I metodi invece sono tipicamente pubblici e restituiscono i valori privati dei campi (o operazioni con essi), per convenzione i nomi iniziano con lettera minuscola e le seguenti parole con iniziale maiuscola. 
>[!warning] RICORDA
>Se un oggetto o un metodo viene definito **statico** significa che è in comune fra tutti gli oggetti di quella classe 

## Costruttore 
Il costruttore è un metodo speciale all'interno di una classe dato che serve a creare gli oggetti, ha il nome uguale a quello della classe, non restituisce nessun valore e all'interno, ha il nome uguale a quello della classe, non restituisce nessun valore e all'interno di una classe ce ne può essere più di uno di solito con parametri diversi. Solitamente al loro interno vengono inizializzati i campi dell'oggetto.
>[!note] Campi e variabili locali
>I campi sono visibili solo all'interno dell'oggetto ed esistono per tutta la sua durata di vita mentre le variabili locali vengono definite all'interno di un metodo o come parametri, una volta terminata la sua eseacuzione queste non esistono più

## Overloading
Accade quando abbiamo metodi con lo stesso nome ma che hanno parametri in input diversi, possiamo utilizzarlo quindi per metodi che svolgono operazioni simili, ma basta fornire il giusto tipo di parametri  per chiamare la definizione corretta.
## Modificatori di visibilità
I campi e metodi di una classe possono essere **pubblici, privati o protetti**, i metodi di una classe possono chiamare sia metodi che campi pubblici o privati della stessa classe, mentre possono chiamare soltanto quelli pubblici di altre classi.
## Oggetti vs Valori Primitivi
Per i valori primitivi la memoria utilizzata è allocata automaticamente a tempo di compilazione mentre per gli oggetti la memoria viene allocata nel momento in cui vengono creati in tempo di esecuzione, inoltre non hanno una dimensione fissa ma lo spazio occupato dipende dai loro campi. In un oggetto a differenza delle variabili locali, i campi vengono inizializzati a dei valori predefiniti, ad esempio i booleani a false, i valori numeri a 0 e oggetti a null.
## Riferimenti ad oggetti
Quando assegniamo un oggetto ad una variabile questa non conterrà l’oggetto ma un **riferimento** ad esso, ovvero l’indirizzo di memoria RAM che lo contiene.
## Metodi Static
Sono dei **metodi di classe** e non **metodi di istanza**, questo significa che possono accedere soltanto ai campi statici (di classe) e non agli oggetti specifici, infatti non è possibile chiamarli tramite degli oggetti.
# Array
Gli array sono una sequenza di elementi dello stesso tipo (sia primitivi che oggetti). Per accedere ad un elemento dell’array dobbiamo specificare il suo indice all’interno della sequenza, non si possono fornire indici maggiori o minori della lunghezza dell’array altrimenti andiamo in contro ad un errore. Se vogliamo modificare le dimensioni di un array possiamo soltanto creare un nuovo array e copiare gli elementi del vecchio tramite il metodo static `Arrays.copyOf()`.
## Matrici
Rappresenta un array bidimensionale, per accedere quindi agli elementi è necessario fornire due indici, possiamo “visualizzarli” come delle tabelle con righe e colonne.
# Confronti
- **`==`**: si utilizza per confrontare l’**identità**, ci si confrontano tipi primitivi oppure i **riferimenti** agli oggetti e non gli oggetti stessi.
- **equals**: Confronto logico, confronta i campi degli oggetti quindi è utilizzabile per quest’ultimi.
- **compareTo**: Serve a comparare due oggetti, restituisce un intero, 0 se i due oggetti sono uguali, < 0 se il primo è minore del secondo e > 0 se il primo è maggiore del secondo.
## Classi Astratte
Sono classi con le quali non possiamo creare oggetti, di solito vengono estese da altre classi che possono invece essere istanziate. All’interno di queste classi possiamo definire **metodi astratti** che non hanno implementazione, le sottoclassi sono **obbligate** a fornirne una, l’unico caso in cui non lo sono è quando sono anche esse astratte.

Quando definiamo una classe con un costruttore non vuoto le sue sottoclassi devono necessariamente chiamarlo tramite **super** nel loro costruttore, se invece non ci sono parametri i costruttori possono anche essere lasciati vuoti impliciti.
## Overriding
L’overriding avviene quando all’interno di una sottoclasse sovrascriviamo l’intera implementazione di un metodo della superclasse lasciando però la stessa intestazione, dobbiamo lasciare gli stessi argomenti, un tipo di ritorno compatibile e non dobbiamo cambiare il livello di visibilità.