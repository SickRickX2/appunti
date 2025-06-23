Gestisce le risorse hardware di un sistema computerizzato (processori, RAM, IO) e fornisce un unsiem di servizi agli utenti.
1) **Processore** si occupa delle computazioni
2) **Memoria principale** è volatile, se il PC si spegne se ne perde il contenuto (chiamata reale o primaria)
3) **IO** memoria secondaria non volatile (dischi), comunicazione (scheda di rete), tastiera ecc...
4) **Registri**
	1) *visibili dall'utente* usati dai linguaggi non interpretati
	2) *di controllo e di stato* usati dal processore per controllare il suo utilizzo, e dal sistema operativo per controllare l'esecuzione dei programmi
	3) *Interni*: usati dal processore, responsabili della comunicazione con memoria e IO
##### Registri visibili all'utente
Sono gli unici che posssono essere usati direttamente quando si prpogramma in un linguaggio macchina. Possono contenere dati o indirizzi (puntatori)
#### Registri interni
I principali registri interni sono:
- *registro di indirizzo di memoria (MAR)* contiene l'indirizzo della prossima operazione di lettura/scrittura
- *registro di memoria temporanea(Memory Buffer Register)* contiene i dati da scrivere in memoria, o lo spazio dove scrivere i dati letti dalla memoria
- *IO address register*
- *IO buffer register* registro di memoria temporanea per IO
#### Registri di controllo e stato
- *Program counter* contiene l'indirizzo dell'istruzione da prelevare dalla memoria
- *Instruction Register* contiene la più recente istruzione prelevata
- *Program Status Word* contiene le informazioni di stato
- *Flag* singoli bit settati dal processore come risultato di operazioni
#### Esecuzione di istruzioni
Due passi:
- fase di *fetch* delle istruzioni: il processore legge il program counter e preleva dalla memoria principale le istruzioni
- fase di *execute* il processore esegue le istruzioni prelevate

## Interruzioni
le interruzioni interrompono la normale esecuzione sequnziale del processo --> come conseguenza viene eseguito software di sistema, parte del sistema operativo.
Le cause sono molteplici, e danno luogo a diverse classi di interruzioni:

>[!note] Interruzioni sincrone
>Interrompono immediatamente il programma 
>- interruzioni da IO
>- interruzioni da fallimento HW
>- interruzioni da comunicazione tra CPU
>- interruzione da timer

>[!note] Interruzioni asincrone
>Vengono sollevate successivamente
>- interruzioni di programma causate da:
>	- overflow
>	- divisione per 0
>	- debugging
>	- errori di riferimenti a memoria
>	- istruzioni errate
>	- syscall
>Vengono chiamate anche **eccezioni/exception**

Per le interruzioni asincrone, una volta che l'handler è terminato, si riprende dall'istruzione successiva a quella interrotta.

Ci sono diversi tipi di errori invece per le sincrone:
- **fault** errore *corregibile*, viene rieseguita la stessa istruzione
- **abort** errore *non corregibile*, si esegue software collegato all'errore
- **trap, system call** di continua dall'istruzione successiva
Quando avviene un interruzione o un eccezione il programma entra in sospensione e vieneeseguita la *interrupt-handler routine*, durante la quale HW e SO collaborano per salvare le informazioni e settare il Program Counter.

