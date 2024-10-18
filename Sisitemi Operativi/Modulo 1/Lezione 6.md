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
>più semplice da realizzare, solo i processi utente possono "vagare". Questo può creare un "bottleneck" perché ci potrebbero essere core più carichi di altri, inoltre se il core del SO fallisce il sistema non può più essere eseguito.
>**Il SO viene eseguito su vari processori:**
>implica un maggior overhead per spostare l'esecuzione del SO

## Scheduling in Linux
Cerca la velocità di esecuzione tramite semplicità di implementazione, non utilizza long term o medium term scheduler. 
C'è però un embrione del long term, quando un processo viene creato viene aggiunto alla coda appropriata o non viene creato affatto (se non viene creato è perchè non c'è abbastanza memoria virtuale).
Essenzialmente è derivato da UNIX quindi *preemptive* a priorità *dinamica*. Abbiamo una specie di round robin con quanto di esecuzione a 1 ms.
Ci sono tre tipi di processi:
- Interattivi: processi utente
- Batch: (non interattivi)
- Real-Time: hanno scadenze temporali ben definite entro cui devono essere terminati, normalmente utilizzati solo dai KLT di sistema
Ci sono tre tipi di scheduling:
- Sched_fifo
- Sched_rr
- Sched_other
La preemption può essere dovuta a due casi:
- un processo passa dallo stato block a running
- si esaurisce il tempo del processo attualmente in esecuzione

# La gestione della Memoria
## Gestione della memoria: requisiti di base
Deve essere incapsulata da una funzione del SO, invisibile ai processi e ai processori. Include anche lo swapping di dati dalla memoria secondaria.
>[!tip] Requisiti
>- **Rilocazione**: importante che ci sia aiuto hardware, *aiuto* e non gestione diretta, sistema operativo e hardware collaborano
>- **Protezione**
>- **Condivisione**
>- **Organizzazione logica**
>- **Organizzazione fisica**

### Rilocazione
Il programmatore non sa e non deve sapere in quale zona della memoria il programma verrà caricato. Potrebbe essere swappato sul disco e al ritorno si trova in una zona diversa di memoria, potrebbe non essere contiguo ecc...
I riferimenti alla memoria devono essere tradotti nell'indirizzo fisico "vero" e abbiamo due modi diversi per farlo.

>[!example] Gli Indirizzi nei Programmi
*Fase di compilazione*
I moduli devono essere pensati come in python, insiemi di funzioni.
Librerie statiche: implementano alcune funzioni che servono per eseguire il codice
>
>*Fase di linking*
>Generazione di codice eseguibile: il *linker* mette tutto insieme tranne le librerie dinamiche. Il risultato si chiama ***load module***.
>
>Il ***load module*** viene caricato dal *loader*, verifica potenziali dipendenze su librerie dinamiche e vengono caricate in memoria principale, se servono a più programmi si utilizzano dei puntatori alla memoria principale in cui si trovano queste librerie.
>>[!note]
>>Ci sono vari modi per la rilocazione in questo caso
>>1)**indirizzi simbolici/logici**: il riferimento in memoria è indipendente dall'attuale posizionamento del programma in memoria
2)**indirizzi assoluti**: si fa un assunzione dalla memoria di partenza e gli indirizzi simbolici vengono aggiornati con indirizzi assoluti della memoria principale
>>3) **indirizzi relativi(usato nei sistemi odierni)**: si assume che si parte da un indirizzo di riferimento e si contano le parole del programma che occupa in memoria e gli indirizzi si aggiornano con questi numerie
### Rilocazione a Run-Time senza Hardware Speciale
Ogni volta che un processo viene riportato in memoria potrebbe essere in un posto diverso

