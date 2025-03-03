
Java è orientato alla programmazione ad oggetti, ogni oggetto:
- Ha uno **stato**, ovvero i suoi **campi**
- Ha la possibilità di compiere azioni
- Appartiene a una **classe** che ne indica il tipo

## Incapsulamento 
Tramite questo metodo andiamo a nascondere i dettagli di un oggetto che non devono essere manomessi ed esponiamo soltanto quello che noi vogliamo.
- L'**interfaccia** è la parte visibile ovvero i *metodi pubblici*.
- L'**implementazione** è quello che manteniamo privato quindi *campi e metodi privati.*

## Ereditarietà
Questo concetto è molto utile per favorire il riutilizzo del codice, una classe madre condivide parte del codice con le sue classi figlie andando ad evitare la riscrittura del codice e la propagazione di errori

Si forma una **gerarchia di classi**:
![[Pasted image 20250205184715.png]]

>[!tip] Extends Impliciti
>In Java qualsiasi classe che creiamo, anche se non estende nessuna classe, in modo implicito estende la classe *Object*, da cui eredita alcuni metodi come **getClass, hashCode, equals.**

## Polimorfismo
Permette di utilizzare lo stesso codice a oggetti di tipo diverso ma che condividono una classe madre. In questo modo possiamo utilizzare il codice della classe madre "generica" senza conoscere necessariamente la classe specifica, se prendiamo l'esempio di prima possiamo creare una lista *Forme* che contiene nello stesso momento oggetti di tipo *Cerchio, Triangolo, Rettangolo* inoltre ne potremmo aggiungere delle altre successivamente senza problemi. Allo stesso modo ogni chiamata ad un metodo invoca la sua implementazione più specifica, ad esempio il metodo **calcolareArea()** se chiamato su oggetti di tipo *Cerchio, Triangolo o Rettangolo* si comporterà in modo diverso, ma è comunque disponibile per tutti gli oggetti di tipo *Forma*.

- Java è orientato agli oggetti
- Java è **cross-platform** (WORA- Write Once, Run Anywhere)
- Java è compilato in bytecode e *interpretato* da una macchina virtuale, queste caratteristiche lo rendono indipendente dalla piataforma. Il codice che noi scriviamo è all'interno di file *.java* questi vengono inviati al compilatore **Javac** 

## Tipi Primitivi 
I tipi primitivi sono **built-in** in Java, li possiamo identificare anche da come sono scritti infatti vengono indicati con l'iniziale minuscola, diversi appunto dalle **classi derivate** che identifichiamo con l'iniziale maiuscola. Alcuni esempi di questi sono:
- **int**- Interi
- **double**- numeri reali
- **boolean**- valori booleani
- **char** - un carattere
- **String**- un "insieme" di caratteri, anche se indicata con la maiuscola viene comunque classificata come tipo primitivo. I tipi permettono anche delle operazioni con comportamento diverso a seconda di esso, ad esempio in una somma fra interi esegue una semplice somma algebrica, mentre una somma stringhe esegue un concatenameanto di queste due.

## Variabili 

Le variabili sono dei nomi che utilizziamo per riferirici a dei valori, queste devono essere dichiarate ad assegnate, è possibile  dichiarare una variabile senza assegnarle un valore, questa rimane appunto indefinita.

>[!note] Scelta dei nomi e CamelCase
>In Java ma in generale nella programmazione si cerca di dare nomi con significato alle variabili, quindi che spieghino cosa contiene e a cosa serve quel valore. Inoltre in Java si cerca di utilizzare la CamelCase (notazione a cammello) quindi:
>- Il nome delle classi ha iniziale maiuscola
>- Il nome delle variabili ha iniziale minuscola

## Letterali 
Per letterale si intende la rappresentazione in codice sorgente di un tipo di dato.
## Espressioni
Un'espressione è un letterale, una variabile o una sequenza di operazioni su letterali e/o variabili che producono un valore. In Java le operazioni hanno delle precedenze, prima vengono eseguite moltiplicazioni, divisioni, resti (%), poi somme e differenze.
## Conversioni di tipo 
Esistono diversi tipi di conversioni:
- **Conversione Esplicita:** Utilizzando un metodo che prende in ingresso uun argomento di un tipo e restituisce un valore di un altro tipo, ad esempio i metodi *Integer.parseInt(), Double.parseDouble(), Math.round()* ecc...
- **Cast Esplicito:** Si scrive il tipo desiderato prima del valore e tra parentesi, quindi scrivendo ad esempio (int) 3.14 otteniamo un valore intero uguale a 3. In questo caso dato che il tipo di partenza era più preciso (double) sono state eliminate le informazioni aggiuntive nel modo più ragionevole, in questo caso togliendo la parte frazionaria.
- **Cast Implicito:** Avviene quando forniamo un valore meno preciso rispetto al tipo dichiarato, Java converte automaticamente al valore più preciso. Ad esempio double num = 2, abbiamo fornito un intero ad un double quindi verrà convertito in 2.0
### Regole per il cast implicito
Questo tipo di cast può avvenire o in fase di **assegnazione** ad esempio da int a long, o da float a double oppure in caso di un'espressione, se è presente un operando double infatti questa viene convertita indouvle, un altro esempio è nel caso di una concatenazione con una stringa che comporta ad un cast a string.




