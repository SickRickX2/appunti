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
>Una pagina viene portata in memoria principale nel momento in cui un qualche processo la richiede, questo comporta a molti page fault durante le prime fasi di vita del proces