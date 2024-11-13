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

## Operazioni Tipiche sui File
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