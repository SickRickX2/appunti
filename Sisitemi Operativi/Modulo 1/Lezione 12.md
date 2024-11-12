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

