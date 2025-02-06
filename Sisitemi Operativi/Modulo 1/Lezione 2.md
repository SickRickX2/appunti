## Interruzioni: sequenziale e annidate
*Sequenziale*:  ne eseguo una dopo l'altra
*Annidate*: se io ho un interruzione e ne arriva un'altra, eseguo prima l'ultima arrivata
## I/O programmato
Le interruzioni vengono principalmente usate per gestire gli input/output.
L'*input/output programmato* è il modo più vecchio per gestirlo, il **processore** è **responsabile** dell'esecuzione del modulo I/O, verifica continuamente se il processo di lettura è completato o meno. Quando viene completata la lettura, i dati vengono spostati nella zona di memoria dedicata all'I/O e quando la scrittura viene completata i dati vengono nuovamente spostati in un'altra zona di memoria e si esegue l'istruzione successiva. Questo metodo è molto poco efficiente.
## I/O da Interruzioni
Un metodo più moderno per fare l'I/O. Il processore non controlla di continuo se viene completato il processo ma esegue altre istruzioni in parallelo che non hanno bisogno di quella lettura. Quando il controller ha spostato i dati viene eseguita un'interruzione per "avvertire" che l'istruzione è stata completata. Non c'è un'inutile attesa perché le interruzioni ci dicono quando i dati sono pronti.
## Accesso diretto in memoria
Il metodo di I/O usato nei computer attuali. Trasferisce un blocco di dati direttamente dalla/alla memoria. Una interruzione viene mandata quando il trasferimento è completato. Permette di fare una scrittura direttamente senza fare una doppia copia; quando viene fatta una richiesta di lettura viene spedita dal processore al DMA (un controller che gestisce il trasferimento diretto di dati), gli dice da che dispositivo inviare i dati e anche dove salvare questi dati.
## Multiprogrammazione
Un processore deve eseguire più programmi contemporaneamente. La sequenza con cui i programmi sono eseguiti dipende dalla loro priorità e dal fatto che siano o meno in attesa di input/output. Alla fine della gestione di un'interruzione, il controllo potrebbe non tornare al programma che era in esecuzione al momento dell'interruzione.
## Gerarchia della memoria
1) Inboard memory: registers, cache, main memory
2) Outboard Storage: Magnetic disk, cd rom, cd rw, dvd rw, dvd ram
3) Offline Storage: magnetic tape
Dall'alto al basso:
 Diminuisce la velocità di accesso, diminuisce i costo al bit, aumenta la capacità e diminuisce la frequenza di accesso alla memoria da parte del processore.
 *Memoria secondaria*: corrisponde all'outboard e all'offline storage, memoria ausiliaria ed esterna, non volatile (se si spegne il computer il contenuto rimane), è usata per memorizzare i files contenenti programmi o dati
 *Memoria cache*: è la memoria più veloce possibile, contiene i dati più usati in modo tale da accedervi nella maniera più veloce possibile. Serve per i dati utili nel breve termine, veloce ma piccola. Segue il principio di località, se uso i dati di a mi serviranno probabilimente i dati di a+1. Mantiene un insieme di dati vicini a quelli usati dalla cpu in modo tale di averli già a disposizione per l'istruzione successiva.
 ![[Pasted image 20240927141127.png]]
 Per il trasferimento dei dati alla cpu non avviene un trasferimento diretto ma passano per la cache, dalla RAM alla cache dopodiché dalla Cache alla CPU. La cache avrà una copia di porzioni della memoria principale. Dobbiamo avere un meccanismo di verifica per vedere se i dati sono già presenti nella cache, e bisogna mantenere una consistenza tra contenuto della cache e contenuto della ram. Generalmente queste cose vengono gestite a livello hardware, perché la cache è fisicamente contenuta nel processore. Nella cache ogni blocco di memoria è indicizzato dalla tag.
 **Lettura della cache:** legge un indirizzo dalla cpu se l'indirizzo non è presente nella cache è un miss che va ricercato nella RAM, viene allocato uno slot per l'indirizzo(o meglio il blocco che lo contiene) che stiamo cercando e in parallelo viene spostato il contenuto del registro ra nella cpu. Se è presente nella cache viene direttamente spedito alla cpu dopo aver fatto il fetch di ra. Cache anche piccole hanno un grande impatto sulle performance. I dati scambiati tra memoria e cache sono in quantità multiple di un blocco, incrementare la misura del blocco aumenta il numero di accessi riusciti, ma incrementarla troppo è controproducente perché aumenta anche il numero di dati da rimuovere, il che abbassa la probabilità di accesso riuscito. La cache utilizza una funzione di mappatura che determina la locazione della cache nella quale andrà messo il blocco proveniente dalla memoria. L'algoritmo di rimpiazzamento sceglie il blocco da rimpiazzare, secondo il *LRU* (least recently used) si rimpiazza il blocco usato meno di recente. La politica di scrittura determina quando occorre scrivere in memoria, può accadere :
 - ogni volta che un blocco viene modificato(write-through)
 - può accadere quando il blocco viene rimpiazzato(write-back)
 occorre minimizzare le operazioni di scrittura, questo vuol dire che la memoria può trovarsi in uno stato "obsoleto". Il SO può fare il flash della cache che ripulisce completamente la cache.

## Servizi offerti da un SO
- Esecuzioni di programmi: applicazioni, servizi
- Accesso ai dispositivi di input/output: filesystem
- Accesso al sistema operativo stesso: shell
- Sviluppo di programmi
- Rilevamento di e reazioni ad errori
- Accounting (chi fa cosa)
## Il kernel
La parte di SO che si trova sempre nella memoria principale. Contiene le funzioni più usate, sta nel "nucleo". 
## Caratteristiche Hardware
Prima di arrivare ai SO moderni si usavano i sistemi Batch. Con le seguenti caratteristiche.
**Protezione della memoria**, non permette che la zona di memoria contenente il monitor venga modificata. 
**Timer**, impedisce che un job monopolizzi l'intero sistema. Istruzioni privilegiate, alcune istruzioni macchina possono essere eseguite solo dal monitor, implementa le interruzioni mentre i primi modelli di computer non le avevano.
- **Protezione della Memoria:** i programmi utente vengono eseguiti in *modalità utente* alcune istruzioni non possono essere eseguite.
- **Il monitor**: viene eseguito in *modalità sistema*, o modalità kernel, le istruzioni privilegiate possono essere eseguite e le aree protette della memoria possono essere accedute
In questo modo più del 96% del tempo è sprecato ad aspettare i dispositivi di I/O.
### Programmazione Singola vs Multiprogrammazione
Singola: il processore dve aspettare che le istruzioni di I/O siano completate prima di procedere.
Multi: se un job deve aspettare che si completi dell'I/O, allora il processore può passare ad un altro job.

## Sistemi Time Sharing
In seguito si è passati ai Sistemi Time Sharing letteralmente sistemi a condivisione di tempo (dagli anni 70).  Implementa l'uso della multiprogrammazione per gestire contemporaneamente più jobs iterattivi, il tempo del processore è condiviso tra più utenti quindi più utenti accedono contemporaneamente al sistema tramite terminali.

|                                       | **Batch**                                                            | **Time Sharing**                    |
| ------------------------------------- | -------------------------------------------------------------------- | ----------------------------------- |
| **Scopo principale**                  | Massimizzare l’uso del<br>processore                                 | Minimizzare il<br>tempo di risposta |
| **Provenienza delle direttive al SO** | Comandi del job control<br>language, sottomessi<br>con il job stesso | Comandi dati da<br>terminale        |

Col passare degli anni si passa dal Job al Processo. Il *processo* riunisce in un unico concetto il job non-interattivo e quello interattivo. Incorpora anche un altro tipo di job che cominciò a manifestarsi dagli anni Settanta: quello transazionale real-time. Un'unità di attività caratterrizzata da: un singolo flusso (thread) di esecuzione, uno stato corrente, un insieme di risorse di sistema ad esso associate.
## Multiprogrammazione dei Processi: Difficoltà
- Errori di sincronizzazione: gli interrupt si perdono o vengono ricevuti 2 volte
- Violazione della mutua esclusione: se 2 processi vogliono accedere alla stessa risorsa, ci possono essere problemi
- Programmi con esecuzione non deterministica: un processo accede ad una porzione di memoria modificata da un altro processo
- Deadlock (stallo): un processo A attende un processo B che attende
**Gestione della memoria**: Utilizza l'isolamento dei processi, una protezione e controllo degli accessi e una gestione automatica di allocazione e deallocazione. Supporto per la programmazione modulare (stack).  Ed è presente una memorizzazione a lungo termine.
**Protezione dell'informazione e sicurezza:** 
- **Disponibilità** (avaibility): il dover proteggere il sistema contro l'interruzione di servizio (DoS attacks)
- **Confidenzialità**: garanzia che gli utenti non leggano informazioni per le quali non hanno l'autorizzazione
- **Integrità dei dati:** protezioni dei dati da modifiche non autorizzate
- **Autenticità:** il dover verificare l'identità degli utenti, o la validità di messaggi e dati
Per quanto riguarda la **pianificazione e la gestione delle risorse** applicano una maggiore *equità (fariness)* dando accesso alle risorse in modo egualitario ed equo e porta ad una *velocità di risposta differenziata* a seconda del tipo di processo. Tutto questo associato ad una maggiore *efficienza* massimizzando l'uso delle risorse per unità di tempo (*throughput*) e minimizzando il tempo di risposta e servire quindi il maggior numero di utenti possibile.
## Struttura del Sistema Operativo
Il sistema viene visto come una serie di livelli, ogni livello effettua un sottoinsieme delle funzioni del sistema e si basa sul livello immediatamente più in basso (che a sua volta effettua delle operazioni di livello più basso). Questo tipo di struttura porta ad una decomposizione del problema in vari sottoproblemi più semplici.

## Architettura di Unix
(questa immagine descrive in generale un SO non solo quelli UNIX)
![[Pasted image 20241001143050.png]]
Il Kernel moderno di Linux è un compromesso tra il kernel *monolitico* ed il *microkernel*.
**monolitico:** kernel tutto in memoria dal boot allo spegnimento
**microkernel:** solo una minima parte del kernel in memoria, il resto caricato quando serve
- sempre in memoria: schedular, sincronizzazione
- solo a richiesta: gestore memoria, filesystem, driver
Quasi tutti i sistemi operativi moderni sono a kernel monolitico (eccezione: Mac OS X).
Linux è principalmente monolitico, ma ha i *moduli*, alcune parti particolari possono essere aggiunte e tolte a richiesta dall'immagine in memoria del kernel. Essenzialmete i diversi file system, i driver per determinati dispositivi di I/O,l'implementazione delle funzionalità di rete