>[!note] ## Scheduling Tradizionale di UNIX
> Combina priorità e una versione di round robin. Ci sono diverse code a seconda delle priorità, all'interno di ciascuna coda utilizza round robin. le priorità vengono ricalcolate ogni secondo, diminuisce la priorità di un processo aumentando il suo tempo di esecuzione (*feedback*).
> Le priorità iniziali sono basate sul tipo di processo.
