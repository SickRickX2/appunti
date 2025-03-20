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
**Sce**