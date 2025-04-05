**Comunicazoine tra processi**
Nel paradigma client/server la *comunicazione* a livello applicazione avviene *tra due programmi applicativi in esecuzione chiamati procesi: un client e un server*.
- Un client è un programma in esecuzione che inizia la comunicazione inviando una richiesta
- Un server è un altro programma applicativo che attende le richieste dai client
### API: Application Programming Interface 
Un linguaggio di programmazione prevede un insieme di istruzioni matematiche, un insieme di istruzioni per la manipolazione delle stringhe, un insieme di istruzioni per la gestione dell'input/output ecc.

Se si vuole sviluppare un programma capace di comunicare con un altro programma, è necessario un **nuovo insieme di istruzioni** per chiedere ai primi quattro livelli dello stack TCP/IP di aprire la connessione, inviare/ricevere dati e chiudere la connessione.

Un insieme di istruzioni di questo tipo viene chiamato **API (Application Programming Interface)**.

>[!note] API di comunicazione
>![[Pasted image 20250405173210.png]]

>[!tip] Comunicazione tra processi: socket
>- Appare come un terminale o un file ma è un'entità fisica
>- Astrazione
>- Struttura dati creata e utilizzata dal programma applicativo
>- Comunicare tra un processo client e un processo server significa comunicare tra due socket create nei due lati di comunicazione.
>
>![[Pasted image 20250405173800.png]]
>![[Pasted image 20250405174312.png]]

### 
