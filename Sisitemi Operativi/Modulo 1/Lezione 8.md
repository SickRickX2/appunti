>[!warning] Ricorda
>I riferimenti alla memoria avvengono tramite **indirizzi logici** tradotti in *indirizzi fisici* a ***tempo di esecuzione***, questo perché un processo potrebbe essere spostato più volte dalla memoria principale alla secondaria e viceversa durante la sua esecuzione, ogni volta occupando zone di memoria diverse.
>Un processo può essere spezzato in più parti, che **non necessariamente** occuperanno una **zona contigua** di memoria principale.

Dall'osservazione che non occorre che tutte le pagine di un processo siano in memoria principale, per far sì che al processo venga concesso il processore, l'unica cosa che serve è che la