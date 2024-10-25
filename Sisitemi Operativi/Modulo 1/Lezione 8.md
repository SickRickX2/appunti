>[!warning] Ricorda
>I riferimenti alla memoria avvengono tramite **indirizzi logici** tradotti in *indirizzi fisici* a ***tempo di esecuzione***, questo perché un processo potrebbe essere spostato più volte dalla memoria principale alla secondaria e viceversa durante la sua esecuzione, ogni volta occupando zone di memoria diverse.
>Un processo può essere spezzato in più parti, che **non necessariamente** occuperanno una **zona contigua** di memoria principale.

Dall'osservazione che non occorre che tutte le pagine di un processo siano in memoria principale  per far sì che al processo venga concesso il processore, ma chel'unica cosa che serve è che la prossima istruzione e i dati di cui ha bisogno siano in memoria principale, si è passati dalla paginazione semplice alla paginazione con memoria virtuale.
>[!example] Esecuzione di un processo
>Il SO porta in memoria principale alcuni pezzi (pagine) del programma. Viene chiamato *resident set* (insieme residente) l'insieme dei programmi che si trovano in memoria principale, viene generato un interrupt quando al processo serve un indirizzo che non si trova in memoria principale (*page fault*). Questa è una richiesta di I/O a tutti gli effetti: il SO mette il processo in modalità blocked.
>>[!tip] Page Fault
>Il pezzo di processo che contiene l'indirizzo logico viene portato in memoria principale, a tal proposito il SO effetua una richiesta di lettura su disco (I/O) e fin quando questa operazione non viene completata un altro processo va in esecuzione, quando l'operazione viene completata, un interrupt farà sì che il processo torni ready. Quando verrà eseguito, occorrerà eseguire nuovamente la stessa istruzione che aveva causato il fault (questa volta la memoria c'è).

>[!warning] Conseguenze
>Svariati processi possono essere in memoria principale, non necessariamente per intero, solo alcune parti per ciascun processo. Questo vuol dire che è molto probabile che ci sia sempre **almeno un processo ready**, quindi il **processore** viene **usato al meglio**. Oltretutto un processo potrebbe anche richiedere più dell'intera memoria principale.
## Memoria virtuale
>[!note] Terminologia 
>*Memoria virtuale:* schema di allocazione di memoria, in cui la memoria secondaria può essere usata come se fosse principale. 
>- gli indirizzi usati nei programmi e quelli usati dal sistema sono diversi
>- c'è una fase di traduzione automatica dai primi nei secondi
>- la dimensione della memoria virtuale è limitata dallo schema di indirizzamento, oltre che dalla dimensione della memoria secondaria
>- la dimensione della memoria principale non influisce sulla dimensione della memoria virtuale
>
>*Indirizzo virtuale:* l'indirizzo associato ad una locazione della virtuale, fa sì che si possa accedere a tale locazione come se fosse parte della memoria principale
>*Spazio degli indirizzi virtuali:* la quantità di memoria virtuale assegnata ad un processo
>*Spazio degli indirizzi:* la quantità di memoria assegnata ad un processo
>la quantità di memoria principale 
>*Indirizzo reale:* indirizzo di una locazione di memoria principale

- Memoria reale: quella principale (RAM) 
- Memoria virtuale: quella secondaria (su disco) 

>[!note] Thrashing
>Letteralmente bastonatura o sconfitta.
>Il SO impiega la maggior parte del tempo a swappare pezzi di processi, anzichè ad eseguire le istruzioni. Quasi ogni richiesta di pagina dà luogo ad una page fault, per evitarlo il SO cerca di prevedere quali pezzi di processo saranno usati con minore o maggiore probabilità

>[!note] Paginazione
>Ogni processo ha una sua tabella delle pagine, ogni entry di questa tabella contiene:
>- il numero di frame in memoria principale 
>- non c'è il numero di pagina, è direttamente usato per indicizzare la tabella 
>- un bit per indicare se è in memoria principale o no
>- un altro bit per indicare se la pagina è stata modificata in seguito all'ultima volta che è stata caricata in memoria princiaple

>[!tip] Caveat 
>La traduzione è fatta dall'hardware, non è una semplice somma ma il numero di pagina va anche moltiplicato per il numero di bytes di ogni singola entry della tabella delle pagine, dopodiché si può sommare.
>Affinchè lo schema funzioni il sistema operativo deve:
>- caricare a partire da un certo indirizzo la tabella delle pagine del processo
>- caricare il valore di in un opportuno registro dipendente dall'hardware (va fatto ad ogni process switch)
