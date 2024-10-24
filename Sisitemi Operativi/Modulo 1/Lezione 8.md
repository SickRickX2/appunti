>[!warning] Ricorda
>I riferimenti alla memoria avvengono tramite **indirizzi logici** tradotti in *indirizzi fisici* a ***tempo di esecuzione***, questo perché un processo potrebbe essere spostato più volte dalla memoria principale alla secondaria e viceversa durante la sua esecuzione, ogni volta occupando zone di memoria diverse.
>Un processo può essere spezzato in più parti, che **non necessariamente** occuperanno una **zona contigua** di memoria principale.

Dall'osservazione che non occorre che tutte le pagine di un processo siano in memoria principale  per far sì che al processo venga concesso il processore, ma chel'unica cosa che serve è che la prossima istruzione e i dati di cui ha bisogno siano in memoria principale, si è passati dalla paginazione semplice alla paginazione con memoria virtuale.
>[!example] Esecuzione di un processo
>Il SO porta in memoria principale alcuni pezzi (pagine) del programma. Viene chiamato *resident set* (insieme residente) l'insieme dei programmi che si trovano in memoria principale, viene generato un interrupt quando al processo serve un indirizzo che non si trova in memoria principale (*page fault*). Questa è una richiesta di I/O a tutti gli effetti: il SO mette il processo in modalità blocked.
>>[!tip] Page Fault
>Il pezzo di processo che contiene l'indirizzo logico viene portato in memoria principale, a tal proposito il SO effetua una richiesta di lettura su disco (I/O) e fin quando questa operazione non viene completata un altro processo va in esecuzione, quando l'operazione viene completata, un interrupt farà sì che il processo torni ready. Quando verrà eseguito, occorrerà eseguire nuovamente la stessa istruzione che aveva causato il fault (questa volta la memoria c'è).
>>[!warning] Conseguenze
>>Svariati processi possono essere in memoria principale, non necessariamente per intero, solo alcune parti per ciascun processo. Questo vuol dire che è molto probabile che ci sia sempre almeno un processo ready 
