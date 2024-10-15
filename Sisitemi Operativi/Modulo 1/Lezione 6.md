>[!note] ## Scheduling Tradizionale di UNIX
> Combina priorità e una versione di round robin. Ci sono diverse code a seconda delle priorità, all'interno di ciascuna coda utilizza round robin. le priorità vengono ricalcolate ogni secondo, diminuisce la priorità di un processo aumentando il suo tempo di esecuzione (*feedback*).
> Le priorità iniziali sono basate sul tipo di processo.

## Architetture Multiprocessore
Ci sono diversi tipi di multiprocessore:
- Cluster
- Processori Specializzati
- Multiprocessore e/o multi-core:
	- condividono la RAM
	- un solo SO controlla tutto

>[!note] 