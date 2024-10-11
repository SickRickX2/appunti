## Condizioni che implicano il quantificatore universale
Fino ad ora abbiamo visto query che implicavano condizioni equivalenti al quantificatore esistenziale: $\exists$ (Esiste almeno un)
Il meccanismo di valutazione consente di rispondere facilmente a questo tipo di query. Infatti, in qualunque posizione appaiono nell'espressione di algebra relazionale, la valutazione delle condizioni avviene in **sequenza**, tupla per tupla. e quando si incontra una tupla che soddisfa le condizioni, questa viene inserita nel risultato. La condizione potrebbe richiedere la valutazione di gruppi interi di tuple prima di decidere se inserirle tutte, qualcuna o nessuna nella risposta e le tuple **non sono ordinate** e la valutazione delle condizioni avviene in **sequenza,tupla per tupla** e una volta inserita una tupla nel risultato **non possiamo più eliminarla**.  In questo caso la condizione equivale a valutare il quantificatore universale:
$\forall


