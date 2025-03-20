Programma di trasferimento file DA/A un host remoto. Comando per accedere ad essere autorizzato a scambiare informazioni  con l'host remoto
```
ftp NomeHost
```
vengono richiesti nome utente e password.

Ci sono comandi per cambiare directory in locale e sull'host remoto, cancellare file, etc.

Modello client/server
- **client**: il lato che inizia il trasferimento
- **server**: host remoto

Quando l'utente fornisce il nome dell'host remoto, il processo client FTP stabilisce una connessione TCP sulla porta 21 con il processo server FTP.
Stabilita la connessione, il client fornisce nome utente e password che vengono inviate sulla connessione TCP come parte dei comandi.
Ottenuta l'autorizzazione del server il client può inviare uno o più file memorizzati nel file system locale verso quello remoto (o viceversa).
![[Pasted image 20250319175210.png]]
**Connessione di controllo**: si occupa delle informazioni di controllo del trasferimento e usa regole molto semplici, così che lo scambio di informazioni si riduce allo scambio di una riga di comando (o risposta) per ogni interazione.
**Connessione dati**: si occupa del trasferimento del file

>[!note] Connessione di controllo
>(Porta 21) Viene usata per inviare informazioni di controllo. L'apertura della connessione di controllo viene richiesta dal client al comando, tutti i comandi eseguiti dall'utente sono trasferiti sulla connessione di controllo. 
>Esempi di informazioni trasferite sulla connessione di controllo:
>- Identificativo utente
>- Password
>- Comandi per cambiare directory
>- Comandi per richiedere invio (put) e ricezione (get) di file
>
>Connessione di controllo: **fuori banda (out of band)** 
>HTTP utilizza la stessa connessione per messaggi di richiesta e risposta e file, per cui si dice che invia le informazioni di controllo "in banda". Il server FTP mantiene lo "stato": directory corrente, autenticazione precedente

>[!note] Connessione dati
>Quando il server riceve un comando per trasferire un file, apre una connessione dati TCP sulla porta 20 con il client. Dopo il trasferimento di un file, il server chiude la connessione.
>La connessione dati viene aperta dal server e utilizzata per il vero e proprio invio del file. Si crea una nuova connessione per ogni file trasferito all'interno della sessione. ![[Pasted image 20250319180239.png|350]]

>[!tip] Risposte FTP
>Le risposte sono composte da due parti: un numero di 3 cifre e un testo. La parte numerica costituisce il codice della riposta, quella di testo contiene i parametri necessari o informazioni supplementari. 

![[Pasted image 20250320104455.png]]
## Posta elettronica
**Scenario classico**
![[Pasted image 20250320105103.png]]
Ci sono tre componenti principali:
- *User agent*: usato per scrivere e inviare un messaggio o leggerlo
- *Message Transfer Agent*: usato per trasferire il messaggio attraverso Internet
- *Message Access Agent*: usato per leggere la mail in arrivo
>[!note] User Agent
>Lo **User Agent** viene attivato dall' utente o da un timer: se c'è una nuova email informa l'utente, viene detto anche *email reader*. 
>Usato per composizione, editing, lettura dei messaggi di posta elettronica.
>I messaggi in uscita o in arrivo sono memorizzati sul server, il messaggio da inviare viene passato al Mail Transfer Agent

>[!note] Message Transfer Agent
> Come comunicano gli MTA:
> - **Server di posta**:
> 	-  *Casella di posta (mailbox)* contiene i messaggi in arrivo per l'utente
> 	- *Coda di messaggi* da trasmettere 
> - **Protocollo SMTP (Simple Mail Transfer Protocol)**: tra server di posta per inviare messaggi di posta elettronica, tra agente utente del mittente e il suo server di posta.

>[!tip] SMTP
>Usa TCP per traferire in modo affidabile i messaggi di posta elettronica dal client al server, porta 25. 
>**Trasferimento diretto** dal server trasmittente al server ricevente.
>Tre fasi per il trasferimento:
>- *Handshaking*
>- trasferimento di messaggi
>- chiusura
>Interazione comando/risposta:
>- **comandi**: testo ASCII
>- **risposta**: codice di stato ed espressione
>
>I messaggi devono essere nel formato ASCII
>![[Pasted image 20250320110540.png]]

### Scambio di messaggi al livello di protocollo
Il client SMTP (che gira sull'host server di posta in invio) da stabilire una connessione sulla porta 25 verso il server SMTP (che gira sull'host server di posta in ricezione)
Se il server è inattivo il client riprova più tardi
Se il server è attivo viene stabilita la connessione
Il server e il client effettuano una forma di handshaking (il client indica indirizzo email del mittente e del destinatario).
Il client invia il messaggio, il messaggio arriva al server desinatario grazie all'affidabilità di TCP.
Se ci sono altri messaggi si usa la stessa connessione (**connessione persistente**), altrimenti il client invia richiesta di chiusura connessione.
 

