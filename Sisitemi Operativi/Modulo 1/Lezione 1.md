Il **Sistema operativo** gestisce le risorse hardware del computer. Il suo scopo è fornire un insieme di servizi agli utenti finali(sviluppatori, utenti base, ecc...) ognuno con esigenze diverse.
Possiamo dire che all'interno di un computer moderno ci sono tre componenti principali:
- CPU
- RAM(Main Memory)
- MODULI DI INPUT/OUTPUT
Per comunicare tra di loro le parti interne vengono collegate tramite i *bus di sistema*.
## Registri del Processorre
Ci sono diversi tipi di registri all'interno del processore:
- *Registri visibili dall'utente:*  usati o da chi programma in assembler o dai compilatori di linguaggi di basso livello/non interpretati, risultano obbligatori per alcune istruzioni su alcuni processori ma facoltativi per ridurre accessi alla memoria principale.
- *Registri di controllo di stato:* vengono usati dal processore per controllare l'uso del processore stesso e dalle funzioni privilegiate del SO per controllare l'esecuzione dei programmi
- *Registri interni:* sono usati dal processore tramite microprogrammazione, essenziali per la comunicazione con memoria e I/O. Sono di fatto gli unici che possono essere usati **direttamente** (con il loro nome) quando si programma in linguaggio macchina (o assembler). Possono contenere dati o indirizzi.
### Registri Interni
- **Registri dell'indirizzo di memoria:** *Memory Address Register (MAR)* contiene l'indirizzo della prossima operazione di lettura/scrittura.
- **Registro di memoria temporanea:** *Memory Buffer Register (MBR)* contiene i dati da scrivere in memoria, o fornisce lo spazio dove scrivere i dati letti dalla memoria
- **Registro dell'indirizzo di input/output:** I/O address register
- **Registro di memoria temporanea per l'input/output:** I/O buffer register
## Registri di controllo di stato
- **Program Counter (PC):** contiene l'indirizzo di un'istruzione da prelevare dalla memoria
- **Instruction Register(IR):** contiene l'istruzione prelevata più di recente
- **Program Status Word (PSW):** contiene le informazioni di stato
- **Codici di condizione (Flag):** singoli bit settati dal processore come risultato di operazioni esempi: risultato positivo, negativo, zero, overflow...
## Esecuzione di Istruzioni
Possiamo riassumere l'esecuzione delle istruzioni in due passi:
1) Il processore legge (preleva, *fase di fetch*) istruzioni dalla memoria
2) Il processore esegue ogni istruzione prelevata
![[Pasted image 20240926212124.png]]
Più approfonditamente, il processore preleva l'istruzione dalla memoria principale. Il PC mantiene l'indirizzo della prossima istruzione da prelevare. Il PC è incrementato dopo ogni prelievo, se l'istruzione contiene un jump, il PC verrà ulteriormente modificato dall'istruzione stessa. Dopodiché l'istruzione viene caricata nell'IR. 
## Interruzioni
Interrompono la normale esecuzione sequenziale del processore, le cause sono molteplici e danno luogo a diverse classi di interruzioni:
- da programma (sincrone)
- da I/O (asincrone)
- da fallimento hardware (asincrone)
- da timer (asincrone)
Le interruzioni da programma sono le uniche sincrone.
### Interruzioni Asincrone
- **Interruzioni da input/output:** generate dal controllore di un disposititivo di input/output che per la maggior parte sono più lenti del processore.
- **Interruzione da fallimento HW:** improvvisa mancanza di potenza (power failure) oppure errore di parità nella memoria
- **Interruzioni da comunicazione tra CPU:** per sistemi in cui ce n'è più di una
- **Interruzioni da timer:** generate da un timer interno al processore, permettono al sistema operativo di eseguire alcune operazioni ad intervalli regolari
### Interruzioni Sincrone
Interruzioni di programma, causate principalmente da:
- overflow
- divisione per 0
- debugging: single step o breakpoint
- riferimento ad indirizzo di memoria fuori dallo spazio disponibile al programma
- riferimento ad indirizzo di memoria momentaneamente non disponibile
Per le interruzioni asincrone, una volta che l’handler è terminato, si riprende dall’istruzione subito successiva a quella dove si è verificata l’interruzione. Questo se la computazione non è stata completamente abortita.
Con le eccezioni sincrone non è detto:
- **faults**: errore correggibile, viene rieseguita la stessa istruzione
- **aborts**: errore non correggibile, si esegue software collegato con l’errore
- **traps** e **system** **calls**: si continua dall’istruzione successiva (sono delle operazioni messe a disposizione dal SO che non interrompono il flusso del programma
>La differenza principale tra sincrone e sincrone è il punto di interruzione e la decisione sull’istruzione successiva.
#### Fase di interruzione
Ad ogni ciclo **fetch-execute**, viene anche controllato se c’è stata un’interruzione ( o una **exception**). Se così è, il programma viene sospeso e viene eseguita una funzione che gestisce l’interruzione. ( *interrupt handler routine*).
L'**interrupt handler** è una funzione particolare: nel programma utente non era prevista. Il SO e Hardware collaborano per salvare alcune informazioni sullo stato del processore in modo tale che dopo la gestione dell’interruzione si possa riprendere da dove si è lasciato (devono essere salvati almeno PC e registro di stato).



