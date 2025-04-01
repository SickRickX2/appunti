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
>[!note] Controllo di flusso
>L'idea è di regolare la quantità di dati inviati al destinatario per non sovraccaricare il buffer di quest'ultimo.
>Per sapere la capacità del destinatario, questa viene comunicata proprio dal destinatario (RWND RcvWindow) nei segmenti header TCP.

>[!note] Controllo della congestione
>Un problema a livello di rete, non tra mittente e destinatario. Lo abbiamo quando abbiamo troppe sorgenti che immettono dati ad una velocità elevata rispetto alla capacità di evasione della rete, conseguentemnete i buffer si riempiono e i pacchetti futuri vengono scartati. Bisogna quindi cercare di diminuire i pacchetti che vengono spediti fin quando non si risolve il problema della congestione e adattarsi di conseguenza.
>Questo è uno dei problemi più studiati e ci sono approcci diversi per risolverlo.
>>[!tip] Metodo end-to-end
>>Nessun sopporto esplicito da parte dei nodi, gli estremi della rete si accorgono della congestione osservando le perdite e i ritardi
>
>>[!tip] Controllo assistito dalla rete
>>i router intermedi forniscono un feedback ai sistemi terminali usando un singolo bit per indicare la congestione

### End to end
- CWND: relativa alla congestione della rete
- RWND: relativa alla congestione del mittente
Dei sintomi di qualche probelma sono **ACK duplicati e timeout**. Se gli ACK arrivano in sequenza e con buona frequenza aumento il rate di trasmissione, se invece ho duplicati e timeout bisogna ridurre la finestra di trasmissione.
L'algoritmo di controllo della congestione si basa su tre componenti
1) Slow start
2) Congestion avoidance
3) Fast recovery
>[!note] Slow start
>CWND inizializzato a 1 MSS, spedisco un segmento, quando arriva l'ack aumento la finestra a 2 quando arriva la ack aumento di 1 e così via. Abbiamo una partenza lenta ma una crescita esponenziale.
>La finestra viene aumentata fino al raggiungimento di una soglia *sshtresh*, dopodiché applico un'altra tecnica

>[!note] Congestion avoidance
>Aumento la finestra di 1 quando mi arriva l'ack di un intero blocco, avendo così un incremento lineare. Incremento la finestra finché non ho timeout o duplicati. Imposto sshtresh a cwnd/2 e imposto la finestra ad 1 ricominciando quindi da capo.

## TCP Taho (o Tahoe)


>[!note] Affinamento
>C'è una correlazione, 3 ACK duplicatiindicano la capacità della rete di consegnare qualche segmento, un timeout prima di 3 ACK duplicati è "più allarmante" perché non sono arrivati nemmeno i pacchetti seguenti.
>Si può quindi distinguere i due tipi di congestione e reagire in maniera più appropriata e meno drastica nel caso dei 3 ack duplicati. 
>Qui entra in gioco il *Fast recovery*; incremento linearmente perché indica una congestione leggera.

## TCP Reno
- Timeout: congestione importante
	- ripartire da 1
- 3 ack duplicati: congestione lieve
	- si raparte da sshtreshold + 3





 



