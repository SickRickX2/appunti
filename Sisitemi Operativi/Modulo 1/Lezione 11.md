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
5) Il modulo di I/O diventa un **processore separato** (*I/O channel*)
6) 

