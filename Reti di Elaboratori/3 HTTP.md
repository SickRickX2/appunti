Ci troviamo all'interno del livello applicativo.
*WWW (World wide web)*: applicazione internet nata dalla necessità di scambio e condivisione di informazioni tra ricercatori universitari di varie nazioni.
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
 >vedi immagine
 
 La risposta dalla parte del server potrebbe fare altre richieste per rispondere al client.
>[!tip]
>Una pagina web è costituita da oggetti: può essre un file html, un'immagine jpeg...
>Una pagina web è formata da un file base HTML che contiene oggetti referenziati (oggeti che si recuperano tramite URL )

>[!note] URL Uniform Resource Locator
>Ci dà le informazioni come:
>- nome
>- locazione della pagina
>- modalità di accesso
>Infatti è composta da 3 parti:
>- protocollo
>- nome della macchina in cui è situata la pagina
>- Il percorso del file che indica la pagina il nome del file e la posizione nel filesystem
>
>Ci possono essere delle piccole deviazoini ad esempio quando la porta non è standard (vedremo più avanti)


 >[!note] Documenti Web
 >- Documento statico
 >- Documento dinamico
 >- Documento attivo: all'interno del file c'è un programma che viene eseguito dal lato client nel momento di visualizzazione
 
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
 >>8) Riceve il nome della richiesta
>>9) cupera il file da disco
 >10)  Invia il file al client
 >11)  Rilascia la connessione
 
 **Connessioni non persistenti**
	 Un solo oggetto viene trasmesso su una connessione TCP

 **Connessione persistente** 
	 Modalità di default, non c'è bisogno di aprire la connessione per ogni oggetto.

>[!note] RTT
>tempo impiegato da un piccolo pacchetto per andare dal client al server e ritornare al client. Include i ritrardi di propagazione.

 **Metodi**
 - POST: serve ad inviare dei dati
 - GET: serve per recuperare un documento dal sever specificato nell'URL (ma si possono anche inviare)
 - HEAD: vogliamo soltanto una porzione del documento
 - PUT: è utilizzato per memorizzare un documento sul server
 **Intestazioni nella richiesta**
 vedi tabella

>[!note] Codici di stato nella risposta
>- 200 OK
>- 301 Moved Permanently: L'oggetto richiesto è stato trasferito
>- 400 Bad Request
>- 404 Not Found

**Intestazioni nella risposta**
altra tabella daiiiiiih

>[!note]




