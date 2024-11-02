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