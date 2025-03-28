Permette di mandare più pacchetti grazie alla pipeline, affidabile, orientato al flusso di dati (mando un flusso continuo di byte), orientato alla connessione (c'è una connessione virtuale e non fisica grazie a informazioni di controllo) e infine gestisce il controllo di flusso e il controllo della congestione.

>[!note] Segmenti TCP
>Il mittente manda dati in maniera continua al destinatario facendo uso del servizio di livello di rete.
>Riceve i dati dal livello applicazione e viene inserita un'intestazione (che in questo caso è molto corposa).
>
>>[!warning] Numero di sequenza
>>Il numero di sequenza è il numero del primo byte di dati contenuti nel segmento. Il numero di riscontro si riferisce al prossimo byte atteso.

>[!tip] FLAGS
>Assumono significato se impostati ad uno:
>Ci sono tre flag che vengono utilizzati per stabilire la connessione.
>- URG: urgent, bisogna vedere il valore del puntatore urgente
>- ACK:
>- PSH: push, bisogna passare i dati a livello applicazione non appena rischiesto
>- RST:
>- SYN:
>- FIN:

## Come stabilire una connessione
Il procedimento si suddivide in tre fasi:
- Apertura dellaconnessione
- trasferimento dati
- Chiusura della connessione

>[!note] Apertura
>3 way handshake
>Se il client vuole aprire una connessione con il server deve mandare una richiesta con il flag syn impostato a 1 ed il resto impostato a 0. C'è inoltre un numero di sequenza per comunicare il numero di sequenza iniziale (scelto in maniera casuale Random ISN). Quando il server riceve la richiesta , manda un ack per accettarla e imposta il flag syn impostato ad uno e manda anche lui un numero di sequenza. Infine il client conferma con un ack il syn del server.

>[!note] Trasferimento dati
>Se il flag urgent è impostato ad uno bisogna vedere il puntatore urgent, non ci dice dove iniziano ma ci dice dove finiscono. Questo serve al destinatario per passare subito questi dati al livello applicazione, ad esempio per interrompere un data transfer.

>[!note] Chiusura della connessione
>Il client (o il server) può chiudere la connessione mediante uno scambio simile a quello di apertura.
>In verità la connessione si può chiudere anche a "metà".

## Controllo degli errori
**Numeri di sequenza** e **ACK**, sono utilizzati per controllare l'errore in un pacchetto di dati.
Solitamente il destinatario mantiene i dati che arrivano fuori ordine ma non li riscontra.
**Checksum** per la correttezza di un segmento
**RTO**: Ack cumulativi e un solo timer associato al più vecchio pacchetto non riscontrato
**Ritrasmissione** del segmento all'inizio della coda di trasmissione

>[!note] ACK cumulativi

Meccanismi adotttati dal TCP
- Pipeline: invia più pacchetti senza dover aspettare l'ack
- Numero di sequenza: del primo byte del segmento
- ACK cumulativo e delayed
- Timeout basato su RTT: unico timer di ritrasmissione.

