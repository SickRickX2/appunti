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
Un dispositivo di input prevede di essere interrogato sul valore di una certa grandezza fisica al suo interno.
- tastiera: codice Unicode degli ultimi tasti premuti 
- mouse: coordinate dell'ultimo spostamento effettuato, quali tasti sono stati premuti
- disco: valori dei bit che si trovano in una certa posizione al suo interno
Un processo che effettua una syscall read su un dispositivo del genere vuole conoscere questo dato..