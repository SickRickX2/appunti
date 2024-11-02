## Elementi Centrali per il progetto del SO 
- Politica di Prelievo (*fetch policy*)
- Politica di posizionamento (*placemet policy*)
- Politica di sostituzione (*replacement policy*)
Il tutto cercando di minimizzarea i page fault; non c'è una politica sempre vincente.

### Fetch Policy
Decide quando una pagina data debba essere portata in memoria principale. Si usano principalmente due politiche :
- paginazione su richiesta (*demand paging*)
- prepaginazione (*prepaging*)

>[!note] Demand Paging
>Una pagina viene portata in memoria principale nel momento in cui un qualche processo la richiede, questo comporta a molti page fault durante le prime fasi di vita del processo

>[!note] Prepaging 
>Porta in memoria principale più pagine di quelle richieste. ovviamente pagine vicine a quella richiesta

### Placement Policy 
Decide dove mettere una pagina in memoria principale quando c'è almeno un frame libero, se non ci sono frame liberi allora **replacement policy**.
Tipicamente il primo frame libero è quello dove viene messa la pagina 
### Replacement Policy
Decide quale pagina sostituire, va fatta in modo da minimizzare la probabilità che la pagina appena sostituita venga subito richiesta di nuovo. Usando il principio di località, si cerca di predire il futuro sulla base del passato recente.
### Gestione del Resident Set
1) *resident set management* propriamente detto, per ogni processo in esecuzione quanti frame di RAM vanno allocati 
2) *replacement scope* decide se quando si rimpiazza un frame bisogna scegliere solo tra i frame che appartengono al processo corrente o un frame qualsiasi
Ci sono due tecniche per ogni problema:
- **allocazione fissa**: il numero di frame è deciso al tempo di creazione di un processo
- **allocazione dinamica**: il numero di frame varia durante la vita del processo, basandosi sulle statistiche che man mano vengono raccolte
>[!note] Replacement Scope
>- Politica locale: se bisogna rimpiazzare un frame si sceglie un altro frame dello stesso processo
>- Politica globale: si può scegliere qualsiasi frame

>[!warning] Attenzione
>Con l'allocazione fissa la politica globale non si può usare

>[!note] Frame bloccati 
*Frame Locking*: se un frame è bloccato non si può sostituire, si fa a livello di kernel del sistema operativo, è sufficiente assegnare un bit ad ogni frame.
Vengono bloccati i frame del sistema operativo ed eventualmente quelli di altri processi.

### Politica di pulitura
Se un frame è stato modificato, va riportata la modifica anche sulla pagina corrispondente. Solitamente viene aggiornata  in un momento che è un compromesso tra quando avviene la modifica e non appena il frame viene sostituito.
## Medium Term Scheduler
Si cerca di aumentare e diminuire il numero di processi attivi, aumentando la multiprogrammazione ma senza arrivare al thrashing.

>[!note ] Algoritmi di Sostituzione
>- Sostituzione ottimale: i sostituisce la pagina che verrà richiesta più in là nel futuro (ovviamente non è implementabile)
>- LRU: sostituisce la pagina a cui non sia fatto riferimento per il tempo più lungo, basandosi sul principio di località dovrebbe essere la pagina che ha meno probabilità di essere usata nel prossimo futuro (implementazione problematica)
>- FIFO: i frame allocati ad un qualunque processo sono trattati come una coda cricolare, le pagine vengono rimosse a turno (implementazione semplice) Si rimpiazzao le pagine che sono state in memoria
>- Clock
