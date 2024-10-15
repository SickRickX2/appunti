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

>[!note] Multiprocessore
>
>**Assegnamento statico:**
>in base allo stato corrente del sistema viene assegnato un processo ad un solo processore per tutta la sua durata. Si può utilizzare uno scheduler per ogni processore
>**Assegnamento dinamico:**
>In questo caso un processo non è legato ad un determinato processore ma può variare in base allo stato delle code di ogni processo, non ci troveremo mai con un processore con una coda piena ed una vuota. Però può provocare complicazioni nella gestione  dei processi.
>**Il SO può esser eseguito sempre su un processore fisso:**
>più semplice da realizzare, solo i processi utente possono "vagare". Questo può creare un "bottleneck" perché ci potrebbero essere core più carichi di altri.
>
