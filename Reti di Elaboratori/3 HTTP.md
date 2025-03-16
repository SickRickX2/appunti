Ci troviamo all'interno del livello applicativo.

*WWW (World wide web)*: applicazione Internet nata dalla necessità di scambio e condivisione di informazioni tra ricercatori universitari varie nazioni.
**Caratteristiche**:
- Opera su richiesta (on demand)
- Facile reperire informazioni
- Diversi motori di ricerca
**Componenti**:
 - Web client (es: browser): interfaccia con l'utente
 - Web server
 - HTML: linguaggio standard per le pagine web
 - HTTP: protocollo per la comunicazione tra client e server
 >[!note] Architettura generale di un browser
 >![[Pasted image 20250316181152.png]]
 
 La risposta dalla parte del server potrebbe fare altre richieste per rispondere al **client**.
 
>[!tip]
>Una pagina web è costituita da **oggetti**: può essere un file HTML, un'immagine JPEG...
>Una pagina web è formata da un file base *HTML (HyperText Markup Language)* che contiene oggetti referenziati (oggeti che si recuperano tramite *URL (Uniform Resource Locator)*

>[!note] URL Uniform Resource Locator
>Ci dà le informazioni come:
>- nome
>- locazione della pagina
>- modalità di accesso
>Infatti è composta da 3 parti:
>- **Protocollo**
>- **Nome della macchina** in cui è situata la pagina
>- Il **percorso del file** che indica la pagina il nome del file e la posizione nel filesystem
>
>Ci possono essere delle piccole deviazoini ad esempio quando la porta non è standard (vedremo più avanti)


 >[!note] Documenti Web
 >- **Documento statico**: contenuto predeterminato memorizzato sul server
 >- **Documento dinamico**: creati dal web server alla ricezione della richiesta 
 >- **Documento attivo**: all'interno del file c'è un programma che viene eseguito dal lato client nel momento di visualizzazione
 
 >[!note] HTTP 
 >Il protocollo è client/server. Il server deve essere in grado di rispondere a più client.
 >>[!tip] Lato Client
 >>1) Il browser determina l'URL ed estrae l'host e il nome del file 
 >>2) Esegue una connessione TCP alla porta 80 dell'host indicato nell'URL
 >>3) Invia richiesta per il file
 >>4) Riceve la risposta
 >>5) Chiude la connessione
 >>6) Visualizza il file
 >
 >
 >
 >>[!tip]  Lato Server
 >>7) Accetta la connessione
 >>8) Riceve il nome del file richiesto
>>9) Recupera il file dal disco
 >10)  Invia il file al client
 >11)  Rilascia la connessione
  
 **Connessioni non persistenti**
	 Un solo oggetto viene trasmesso su una connessione TCP, ciascuna coppia richiesta/risposta viene inviata su una connessione TCP separata. 

 **Connessione persistente** 
	 Modalità di default, non c'è bisogno di aprire la connessione per ogni oggetto, quindi più oggetti possono essere trasmessi su una singola connessione TCP tra client e server.

>[!note] RTT Round Trip Time
>Tempo impiegato da un piccolo pacchetto per andare dal client al server e ritornare al client. Include i ritardi di propagazione, di accodamento e di elaborazione del pacchetto.

>[!example] Formato generale dei messaggi di richiesta HTTP
>![[Pasted image 20250316183807.png]]

 **Metodi**
 - *POST*: serve ad inviare dei dati
 - *GET*: serve per recuperare un documento dal sever specificato nell'URL (ma si possono anche inviare)
 - *HEAD*: vogliamo soltanto una porzione del documento
 - *PUT*: è utilizzato per memorizzare un documento sul server
 **Intestazioni nella richiesta**
 ![[Pasted image 20250316184542.png]]

>[!note] Codici di stato nella risposta
>- 200 OK
>- 301 Moved Permanently: L'oggetto richiesto è stato trasferito
>- 400 Bad Request
>- 404 Not Found

**Intestazioni nella risposta**
altra tabella daiiiiiih

## Cookie 
Il protocollo HTTP è detto senza stato, se un client fa più richieste allo stesso server, il server tratta le richieste in maniera indipendente. Non c'è alcuna correlazione tra richieste consecutive dallo stesso cliente nello stesso server e quindi non mantiene informazioni sulle richieste fatte.

Ci sono casi in cui si vorrebbero salvare gli stati, ad esempio per offrire un contenuto personalizzato in base al profilo dell'utente.

Gli indirizzi IP degli host non sono adatti.
La soluzionee sono i *cookie*.

>[!note] Cookie
>Si cerca di creare una sorta di "sessione", va oltre alla singola risposta ma collega risposte provenienti dallo stesso client. 
>Ogni sessione ha:
>1) un inizio ed una fine
>2) un tempo di vita
>3) Sia il client che server possono chiuder la sessione
>4) è implicita nello scambio di informazioni di stato
>
>Ci sono 4 componenti:
>- Riga di intestazione nel messaggio di risposta
>- riga intestazione nel messaggio di richiesta
>- file cookie mantenuto sul sistema terminale dell'utente e gestito dal browser dell'utente
>- un database sul server
>
>Il server mantiene tutte le informazioni riguardanti il client su un file e glia assegna un identificatore che viene fornito dal client.
>- Il cli
>**Durata di un cookie**: è a discrezione del server, viene attribuita un attributo chiamato Max-age
>**Cosa possono contenere i cookie**:
>- preferenze dell'utente
>- carta per acquisti
>- autorizzazione
>
>**Privacy**: mantenendo il profilo sul server costituisce un problema per la privacy.

## Web caching
Serve a migliorare le prestazioni della navigazione in tempi di risposta.
Si può fare a livello di browser o proxy
>[!note] Browser
>Il browser mantiene la cache delle pagine visitate (quindi è locale e non serve una richiesta al server).

>[!note] Proxy
>Viene fatta ad un livello più alto, una macchina dedicata per le richieste degli utenti. Il server proxy copia le pagine visitate e al momento di richiesta vengono restituite se contenute altrimenti si chiede direttamente al server. Però bisogna controllare che la pagina del proxy sia ancora "aggiornata", quindi non è immediata.

>[!danger] Inserimento di un oggetto in cache
> Il client invia un messaggio di richiesta alla cache, se non ha l'oggetto fa la richiesta la server di origine, quest'ultimo manderà la risposta con intestazione last modified. Successivamente se viene richiesta la pagina risulta valida in locale. 
> A questo punto la cache chiede al server per verificare se l'oggetto è ancora valido tramite il metodo *get condizionale*. Riceve una risposta solo se l'oggetto non è stato modificato, altrimenti verrà memorizzato in cache l'oggetto nuovo.











