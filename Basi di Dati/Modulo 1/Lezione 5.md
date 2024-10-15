## Condizioni che implicano il quantificatore universale
Fino ad ora abbiamo visto query che implicavano condizioni equivalenti al quantificatore esistenziale: $\exists$ (Esiste almeno un)
Il meccanismo di valutazione consente di rispondere facilmente a questo tipo di query. Infatti, in qualunque posizione appaiono nell'espressione di algebra relazionale, la valutazione delle condizioni avviene in **sequenza**, tupla per tupla. e quando si incontra una tupla che soddisfa le condizioni, questa viene inserita nel risultato. La condizione potrebbe richiedere la valutazione di gruppi interi di tuple prima di decidere se inserirle tutte, qualcuna o nessuna nella risposta e le tuple **non sono ordinate** e la valutazione delle condizioni avviene in **sequenza,tupla per tupla** e una volta inserita una tupla nel risultato **non possiamo più eliminarla**.  In questo caso la condizione equivale a valutare il quantificatore universale:
$\forall$
oppure
$\nexists$

Quindi quando ci troviamo di fronte ad un problema del tipo:
*Nomi e città dei clienti che hanno SEMPRE
ordinato più di 100 pezzi per un articolo*
Bisogna ragionare usando una doppia negazione:
>[!warning] Ricorda
>La negazione di *per ogni* non è *per nessuno* ma *almeno un elemento non*
>>[!example]
>>La negazione di "**Tutti** i miei amici si chiamano Paolo" non è "**Nessun** amico si chiama Paolo" ma "Ho **un** amico che non si chiama Paolo"

Quindi quando ci si trova di fronte ad una query di quel tipo, bisogna eseguire la query con la condizione negata
