# La gestione dell'Input/Output
Area molto problematica per la progettazione di sistemi operativi
- c'è una grande varietà di dispostivi I/O
- grande variet di applicazioni che li usano
- difficile scrivere un SO che tenga conto di tutto
Ci sono tre categorie di dispositivi:
- leggibili dall'utente 
- leggibili dalla macchina 
- dispositivi di comunicazione

>[!note] Dispositivi Leggibili dall'Utente
>Dispositivi usati per la comunicazione diretta con l'utente 
>- stampanti
>- terminali(monitor, tastiera, mouse)
>- joystick
>- ...

>[!note] Dispositivi Leggibili dalla Macchina 
>Dispositivi usati per la comunicazione con materiale elettronico
>- dischi 
>- chiavi USB 
>- sensori
>- controllori
>- attuatori

>[!note] Dispositivi per la Comunicazione
>Dispositivi usati per la comunicazione con dispositivi remoti
>- modem
>- schede Ethernet
>- Wi-Fi

### Funzionamento
>[!note] Input
Un *dispositivo di input* prevede di essere interrogato sul valore di una certa grandezza fisica al suo interno.
>- tastiera: codice Unicode degli ultimi tasti premuti 
>- mouse: coordinate dell'ultimo spostamento effettuato, quali tasti sono stati premuti
>- disco: valori dei bit che si trovano in una certa posizione al suo interno
>
Un processo che effettua una **syscall read** su un dispositivo del genere vuole conoscere questo dato..

>[!note] Output
>Un dispositivo di output prevede di poter cambiare il valore di una certa grandezza fisica al suo interno
>- monitor moderno: valore RGB di tutti i suoi pixel
>- stampante moderna: PDF o PS di un file da stampare 
>- disco: valore dei bit che devono sovrascrivere quelli che si trovano in una certa posizione al suo interno
>
>Un processo che effetua una **syscall write** su un dispositivo del genere vuole cambiare qualcosa.

## Tecniche per effettuare l'I/O
- Programmato
- Guidato dagli interrupt
- Accesso diretto in memoria(DMA)

|                             | **Senza interruzioni** | **Con interruzioni**           |
| --------------------------- | ---------------------- | ------------------------------ |
| **Passando per la CPU**     | I/O programmato        | I/O guidato dalle interruzioni |
| **Direttamente in memoria** |                        | DMA                            |

### Direct Memory Access
Il processore delega le operazioni di I/O al modulo DMA. Il modulo DMA trasferisce i dati direttamente da o verso la memoria principale. Quando l'operazione è completata il modulo DMA genera un interrupt per il processore. In sostanza permette di copiare un blocco di memoria direttamente senza passare per la CPU.

##  Evoluzione della Funzione di I/O
1) Il **processore controlla** il dispositivo periferico
2) Viene **aggiunto un modulo** (o controllore) di I/O direttamente sul dispositivo senza interrupt
3) **Modulo** o controllare di I/O **con interrupt**, migliora l'efficienza del processore che non deve aspettare il completamento dell'operazione I/O
4) **DMA**: blocchi di dati viaggiano tra dispositivo e memoria senza usare il processore che fa qualcosa solo all'inizio e alla fine dell'operazione
5) Il modulo di I/O diventa un **processore separato** (*I/O channel*), il processore principale comanda questo per eseguire un certo programma I/O in memoria principale
6) **Processore per l'I/O**, ha una sua memoria dedicata, viene usato per le comunicazioni con terminali interattivi

Durante la progettazione bisogna prestare attenzione ad alcuni punti:
- *Efficienza*: per fare in modo che i dispositivi I/O, essendo molto lenti rispetto alla memoria principale, non rallentino il processore
- *Generalità*: Anche se diversi tra loro bisognerebbe gestire i dispositivi I/O in maniera uniforme

Bisogna quindi approcciare una **progettazione gerarchica**.  Per l'I/O ci sono 3 macrotipi maggiormente usati per l'implementazione a livelli 
>[!note] **Dispositivo Locale**
> (stampante, monitor, tastiera) 
> - Logical I/O: il dispositivo viene visto come una richiesta logica
> - Device I/O: trasforma richieste logiche in sequenze di comandi di I/O
> - Scheduling and Control: esegue e controlla le sequenze di comandi eventualmente gestendo l'accodamento

>[!note] **Dispositivo di Comunicazione**
>(scheda Ethernet, WiFi, ...)
>Come quello locale ma al posto del logical c'è un dispositivo per la comunicazione

>[!note] **File System**
>(vari dischi, USB key, ...)
>- Directory Management: tutte le operazioni utente che hanno a che fare con i file
>- File System: struttura logica delle operazioni
>- Organizzazione fisica: da identificatori di file a indirizzi fisici su disco; allocazione/ deallocazione

## Buffering dell'I/O

## Come Funziona un disco
I dati si torvano sulle tracce e all'interno delle tracce ci sono settori che contengono una determinata quantità di dati. La lettura fisica viene attrverso una testina magnetica che rileva il valore di un singolo bit (se magnetizzato 1 altrimenti 0). Il disco ruota fisicamente per far leggere i diversi settori.
L'*Access time*, è la somma di:
- **seek time**: tempo della testina
- **rotational delay**: tempo di rotazione
- **transfer time**: tempo di trasferimento dei dati
A parte:
- *wait for device*: attesa che il dispositivo sia asseganto alla richiesta
- *wait for channel*: attesa che il sottodispositivo sia assegnato alla richiesta 


>[!note] Politiche di scheduling
>- random: il peggiore
>- FIFO: simile al random
>- Priorità: non ottimizza effetivamente il discoe non è equo ma permette di raggiungere altri obiettivi
>- LIFO: last in first out, buono per DBMS con transazioni, ma non è un algoritmo genericamente buono (non ha molto senso in situazioni generiche)
>- SSTF: shortest service time first, bisogna sapere la posizione della testina per decidere quale richiesta successiva soddisfare, sfrutta il disco al massimo ma non è equo, quindi c'è un alto rischio di starvation
>**Algoritmi migliori**
>- SSCAN: cerca di ottimizzare il movimento della testina in modo tale che il braccio si muova sempre in un verso(avanti fino alla fine e indietro  fino all'inizio del disco), non c'è starvation ma è poco equo.
>- C-SCAN: funziona allo stesso modo con una piccola modifica, quando torniamo indietro con il braccio non soddisfiamo nessuna richiesta il che lo rende più equo ma meno ottimizzato
>- F-SCAN: abbiamo due code separate, accumulo le richieste in coda F e uso l'algoritmo SCAN per servirle, tutte le nuove richieste vengono aggiunte alla coda R. Quando SCAN finisce F ed R si invertono. Quindi le nuove richieste non possono passare avanti a quelle più vecchie.
>- N-step-scan: aumentando il numero delle code aumentiamo l'efficienza del disco

### SSD
Struttura: stack (pila) di flash chips organizzati in matrici, che allora volta hanno dei piani (planes suddivisi in blocchi composti da pagine), in cui vengono salvati i dati.
- In lettura: possiamo aaccedere alle pagine
- In scrittura: non è possibile sovrascrivere le pagine ma bisogna azzerare tutte le pagine di quel blocco, avendolo prima copiato e poi riscritto con la parte nuova. Nel blocco vecchio viene salvata la versione precedente mentre in quello nuovo c'è sia la vecchia informazione  che quella nuova
![[Pasted image 20241108151512.png]]
Gli SSD sono estremamente veloci. nessun tempo richiesto per il seek

## Cache del disco
Contiene una copia di acluni settori letti dall' hard disk, che verrà usata in memoria principale. Ci sono diversi modi per decidere come gestire la cache.
- *LRU* quello con la reference meno recente a quel settore
- *LFU* quello con meno reference a quel settore
- Sostituzione basata su Frequenza: stack diviso in due una parte nuova e una vecchia, una parte usa LRU (la vecchia) e una LFU(la nuova). L'idea  è quella di proteggere i settori "nuovi" che vengono utilizzati e vengono rimossi solo quando non vengono utilizzati e poi quando hanno poche reference
- Sostituzione basata su Frequenza a 3 segmenti:
	- nuovo: non eleggibile per il rimpiazzamento
	- medio: contatori vengono incrementati ma i settori non possono essere  rimpiazzati
	- vecchio: vengono eliminati quelli che non vengono usati e hanno un contatore di referenze basse