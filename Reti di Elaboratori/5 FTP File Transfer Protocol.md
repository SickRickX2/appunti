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


