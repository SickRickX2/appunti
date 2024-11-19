# Il File System
>[!note] I Files
>Sono l'elemento principale per la maggior parte delle applicazioni, molto spesso l'input di un'applicazione è un file. I file "sopravvivono" ai processi.

Il file è una delle parti del sistema operativo che sono più importanti per l'utente.
Proprietaà desiderabili:
- esistenza a lungo termine
- condivisibilità con altri processi (tramite nomi simbolici)
- strutturabilità (directory gerarchiche)

I programmi che gestiscono i file costituiscono il ***File Management System*** e vengono eseguiti come processi privilegiati (kernel mode). Le librerie invece a vengono invocate come system call. 
Per ogni file vengono mantenuti degli attributi(o metadati), come proprietario, data di creazione, ecc...

#### Operazioni Tipiche sui File
- Creazione
- Cancellazione
- Apertura
- Lettura
- Scrittura
- Chiusura

>[!note] Campi
>Sono dati di base che contengono valori singoli. caratterizzati da una lunghezza e tipo di dato (es: carattere ASCII)

>[!note] Record
>Sono insiemi di campi correlati, ognuno trattato come un'unità (es: record-nome, cognome, matricola, stipendio)

>[!note] File
>Hanno un nome, insiemi di record correlati. Possono implementare meccanismi di controllo dell'accesso

>[!note] Database
>Collezioni di dati correlati che mantengono anche relazioni tra gli elementi memorizzati. Realizzati con uno o più file.

I File Management Systems forniscono servizi agli utenti e alle applicazioni per l'uso di file, definiscono anche il modo in cui i file sono usati. Permettono ai programmatori di non scrivere codice per gestire i file.
#### Obiettivi per i FMS:
- Rispondere alle necessità degli utenti riguardo alla gestione dei dati
- Garantire che i dati nei file sono validi
- Ottimizzare le prestazioni
- Fornire supporto per diversi tipi di memoria secondaria
- Minimizzare i dati persi o distrutti
- Fornire un insieme di interfacce standard per i processi utente
- Fornire supporto per l'I/O effettuato da più utenti in contemporanea
#### Requisiti per i FMS:
1) Ogni utente dev'essere in grado di creare, cancellare, leggere scrivere e modificare un file
2) Ogni utente deve poter accedere in modo controllato ai file di un altro utente
3) Ogni utente deve poter leggere e modificare i permessi di accesso ai propri file
4) Ogni utente deve poter ristrutturare i propri file in modo attinente al problema affrontato
5) Ogni utente deve poter muovere dati da un file ad un altro
6) Ogni utente deve poter mantenere una copia di backup dei propri file
7) Ogni utente deve poter accedere ai propri file tramite nomi simbolici


#### Organizzazione del codice

>[!note] Directory Management
>Da nomi di file a identificatori di file; tutte le operazioni utente che hanno a che fare con i file (crearli, cancellarli, spostarli)

>[!note]  File System
>Struttura logica ed operazioni

>[!note]  Organizzazione fisica
>Da identificatori di file a indirizzi fisici su disco: allocazione/deallocazione

>[!note] Scheduling & Control: 
ovviamente è qui che ci  sono i vari SCAN e compagnia bella

## Le directory
Le directory contengono varei informazioni sui file come:
- attributi
- posizione (dove sono i dati)
- proprietario
Una directory è essa stessa un file (speciale), fornisce il mapping tra nomi dei file e file stessi
>[!example] Operazioni 
>- Ricerca
>- Creazione file
>- Cancellazione file
>- Lista del contenuto della directory
>- Modifica della directory

Ci sono vari elementi delle Directory
- **Informazioni di base**: nome del file, tipo del file, organizzazione del file
- **Informazioni sull'indirizzo**: volume(dispositivo su cui il file è memorizzato), indirizzo di partenza, dimensione attuale, dimensione allocata
- **Controllo di accesso**: proprietario, informazioni sull'accesso, azioni permesse
- **Informazioni sull'uso**: data di creazione, identità del creatore, data dell'ultimo accesso in lettura, data dell'ultimo accesso in scrittura, identità dell'ultimo lettore, identità dell'ultimo scrittore, data dell'ultimo backup, uso attuale

Il metodo usato per memorizzare le informazioni di cui sopra varia molto da sistema a sistema. Quello più semplice è fare una lista di entry, una per ogni file.
Ci sono due problemi  importanti:
1) non aiuta nell'organizzare i file
2) non si può dare lo stesso nome a due file diversi
>[!note] Schema a due livelli per le directory
Una directory per ogni utente, più una (master) che le contiene, la master contiene anche l'indirizzo e le informazioni per il controllo all'accesso. Ogni directory utente è solo una lista dei file di quell'utente, quindi non offre una struttura per insiemi di files

>[!note] Schema gerarchico ad albero per le Directory
>Una *directory master* che contiene le directory utente. Ogni directory utente può contenere file oppure altre directory utente. Ci sono anche sottodirectory di sistema, sempre dentro la directory master
>![[Pasted image 20241114210336.png]]

>[!tip]  Nomi
>Gli utenti devono potersi riferire ad un file usando solo il suo nome, i nomi devono essere unici, ma un utente può non aver accesso a tutti i file dell'intero sistema
>La struttura ad albero permette agli utenti di trovare un file seguendo un percorso nell'albero (*directory path*)
>-  nomi duplicati sono possibili purché abbiano path diversi

#### Directory di lavoro
Dover dare ogni volta il path completo prima del nome del file può essere lungo e noioso. Solitamente gli utenti o processi interattivi hanno associata una directory di lavoro o corrente. Tutti i nomi di file sono dati relativamente a questa directory ed è sempre possibile dare esplicitamente l'intero percorso, se neccessario

## Gestione della Memoria Secondaria
Il SO è responsabile dell'assegnamento di blocchi a file.
Da qui nascono due problemi:
 - occorre allocare spazio per i file, e mantenerne traccia una volta allocato
 - occorre tener traccia dello spazio allocabile
 I file si allocano in "porzioni" o "blocchi"
 - l'unità minima è il settore del disco
 - ogni porzione o blocco è una sequenza contigua di settori
>[!note] Preallocazione vs Allocazione dinamica
>**Preallocazione**: la massima dimensione è dichiarata a tempo di creazione. Questo metodo porta ad uno spreco di spazio su disco, a fronte di un modesto risparmio di computazione
>**Allocazione dinamica**: quasi sempre preferita, la dimensione viene aggiustata in base alle append o alle truncate. Ci sono due possibilità agli estremi:
>1) Si alloca una porzione larga a sufficienza per l'intero file, efficiente per il processo che vuole creare il file: l'accesso sequenziale è il più veloce 
>2) Si alloca un blocco alla volta, efficiente per il SO che deve gestire tanti file
>
>Si cerca un punto di incontro tra efficienza del sistema operativo e efficienza del singolo file. Ci sono dunque due possibilità valide sia per la preallocazione che per l'allocazione dinamica:
> 1) Porzioni gandi e di dimensione variabile, dove ogni singola allocazione è contigua, ma è complicata la gestione dello spazio libero
> 2) Porzioni fisse e piccole: tipicamente un blocco per porzione, molto meno contiguo del precedente

>[!example] Preallocazione + porzioni grandi e di dimensione variabile
>Se si usa questa combinazione, niente tabella di allocazione: per ogni file basta l'inizio e la lunghezza. Ogni file è un'unica porzion. Ma è inefficiente per lo spazio libero, necessita periodica compattazione, il che è molto oneroso

#### Come allocare spazio per i File
Ci sono tre metodi
- Contiguo
- Concatenato
- Indicizzato
>[!note] Allocazione Contigua
>Un insieme di blocchi viene allocato per il file quando quest'ultimo viene creato. In questo caso la preallocazione è necessaria, ma allo stesso tempo sarà necessaria una sola entry nella tabella di allocazione dei file