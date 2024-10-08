# Strutture di Controllo del SO
Il SO è l'entità che gestisce l'uso delle risorse di sistema da parte dei processi, in primis il processore. Poiché il SO deve gestire sia i processi che le risorse, deve conoscere lo stato di ogni processo e di ogni risorsa. Per ogni entità da gestire il SO costruisce e mantiene una o più tabelle.
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
>**Identificatori:**
>- del processo (PID)
>- del processo padre (Parent PID o PPID)
>
**Informazioni sullo stato del processore:**
>- registri utente (accessibili in linguaggio macchina/assembler)
>- program counter
>- stack pointer
>- registri di stato: risultati di operazioni aritmetico/logiche, modalità di esecuzione, interrupt abilitati/disabilitati
>- 
>**Informazioni per il controllo del processo:**
>- stato del processo (ready, suspended, blocked, ...)
>- priorità
>- informazioni sullo scheduling (ad esempio per quanto tempo è stato in esecuzione l'ultima volta)
>- l'evento da attendere per tornare ad essere ready se attualmente in attesa
>
>**Supporto per strutture dati:**
>- puntatori ad altri processi
>- per mantenere liste concatenate di processi nei casi in cui siano necessarie (ad esempio code di processi per qualche risorsa)
>
>**Comunicazioni tra processi:** flag, segnali. messaggi per la comunicazione tra processi
>**Permessi speciali**: non tutti i processi possono accedere a tutto
>Gestione della memoria: puntatori ad aree di memoria che gestiscono l'uso della memoria virtuale
>**Uso delle risorse**

Possiamo dire che il  PCB è la struttura dati più importante di un sistema operativo poiché definisce lo stato del SO stesso. Proprio per questo motivo richiede  delle protezioni, una funzione scritta male potrebbe infatti danneggiare il blocco, rendendo il SO incapace di gestire i processi. Ogni cambiamento nella progettazione del blocco ha effetti su molti moduli del SO.
>[!tip] Modalità di Esecuzione
>La maggior parte die processori supporta almeno due modalità di esecuzione.
>**Modo sistema**: pieno controllo, si può accedere a qualsiasi locazione di RAM, per il kernel
>**Modo utente**: molte operazioni sono vietate, per i programmi utente

>[!warning] Kernel Mode
Viene usata per le operazioni effetuate dal kernel. Gestisce i processi tramite il PCB, gestisce la memoria principale allocando lo spazio per i processi, gestisce l'I/O e assegna le loro risorse ai processi e ha delle funzioni di supporto come gestione delle eccezioni, accounting e monitoraggio.


## Da User Mode a Kernel Mode e Ritorno
Questo è uno schema con il quale un processo utente può cambiare la modalità a sé stesso, ma solo per eseguire software di sistema. Il codice può essere eseguito da tre entità:
- Per conto  dello stesso processo interrotto, che non lo ha esplicitamente voluto e allora si ricade in due casi *abort* o *fault*
- Per conto dello stesso processo interrotto, che lo ha esplicitamente voluto e questo può essere causato da una system call o in risposta ad una sua precedente richiesta di I/O
- Per conto di un qualche altro processo in risposta ad una sua precedente richiesta di I/O o comunque di risorse

>[!note] Creazione di un Processo
>Per creare un processo il SO deve:
>1) assegnargli un PID unico
>2) allocargli spazio in memoria principale
>3) inizializzare il process control block
>4) inserire il processo nella giusta coda
>5) creare o espandere altre strutture dati

>[!warning] Ricorda
>Bisogna considerare che c'è una differenza tra switch di modalità di un processo e switching di processi.
>**Switch di modalità:** da modalità utente a sistema e viceversa
>**Switching tra processi:** per qualche motivo l'attuale processo non deve più usare il processore, che va concesso invece ad un altro processo

Il Sistema Operativo può riprendere il controllo, togliendolo al processo attualmente in esecuzione per diversi motivi:

| **Meccanismo** | **Causa**                                           | **Uso**                                 |
| -------------- | --------------------------------------------------- | --------------------------------------- |
| Interruzione   | *Esterna* all'esecuzione dell'istruzione corrente   | Reazione ad un evento esterno asincorno |
| Eccezione      | Associata all'esecuzione dell'*istruzione corrente* | Gestione di un errore sicnrono          |
| Chiamata al SO | *Richiesta* esplicita                               | Chiamata a funzione di sistema          |


