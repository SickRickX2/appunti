# Strutture di Controllo del SO
Il SO è l'entità che gestisce l'uso delle risorse di sistema da parte dei processi, in primis il processore. Poiché il SO deve gestire sia i processi che le risorse, deve conoscere lo stato di ogni processo e di ogni risorsa. Per ogni entità da gestirer il SO costruisce e mantiene una o più tabelle.
>[!note] Tabelle di Memoria
>Le tabelle di memoria sono usate per gestire sia la memoria principale che quella secondaria, quest'ultima come vedremo più avanti serve per la memoria virtuale. Devono comprendere le seguenti informazioni:
>- allocazione di memoria principale da parte dei processi
>- allocazione di memoria secondaria da parte dei processi
>- attributi di protezione per l'accesso a zone di memoria condivisa
>- informazioni per gestire la memoria virtuale

>[!note] Tabelle per l'I/O
>Vengono usate dal SO per gestire i dispositivi e i canali di I/O. Devono comprendere le seguenti informazioni:
>- se il dispositivo è disponibile o già assegnato
>- lo stato dell'operazione di I/O
>- la locazione in memoria principale usata come sorgente o destinazione del trasferimento di I/O

>[!note] Tabelle dei File
>Queste tabelle forniscono informazioni su:
>- esistenza dei files
>- locazioni in memoria secondaria
>- stato corrente
>- altri attributi
>Vengono memorizzate parte su disco e parte in RAM

>[!note] Tabelle dei Processi
>Per gestire i processi il SO deve conoscerne i dettagli:
>- stato corrente
>- identificatore
>- locazione in memoria
>- etc
>All'interno vi è il Blocco di controllo del processo (Process Control Block PCB), le informazioni in esso contenute sono spesso chiamate *attributi del processo*.
>Si dice **process image** (immagine del processo) l'insieme di programma sorgente, dati, stack delle chiamate e PCB

## Attributi dei processi
Le informazioni in ciascun blocco di controllo possono essere raggruppate in 3 categorie: 
- identificazione
- stato
- controllo
**Come si identifica un processo?**
Ad ogni processo è assegnato un numero identificativo, quindi unico: il *PID* (Process Identifier).
Molte tabelle del SO usano i PID per realizzare collegamenti tra le varie tabelle e la tabella dei processi. Ad esempio quella dei I/O deve mantenere, per ogni dispositivo, quale processo lo sta usando. Basta mettere il PID, e implicitamente si può accedere alle informazioni sul processo corrispondente.
>[!tips] Lo stato del processore
>Da non confondere con lo stato, o meglio la modalità del processo (ready, blocked, ...). E' dato dai contenuti dei registri del processore stesso:
>- registri visibili all'utente
>- registri di controllo e di stato
>- puntatori allo stack
>Il **Program Status Word(PSW)** contiene le informazioni di stato.

>[!note] Control Block del Processo
>Contiene le informazioni di cui il SO ha bisogno per controllare e coordinare i vari processi attivi. 
>Identificatori:
>- del processo (PID)
>- del processo padre (Parent PID o PPID)
>
Informazioni sullo stato del processore:
>- registri utente (accessibili in linguaggio macchina/assembler)
>- program counter
>- stack pointer
>- registri di stato: risultati di operazioni aritmetico/logiche, modalità di esecuzione, interrupt abilitati/disabilitati
>Informazioni per il controllo del processo:
>- stato

