Siamo al livello di trasporto, 
Protocolli di trasporto forniscono la *comunicazione logica* tra processi applicativi di host differenti. Come se fossero connessi direttamente anche se non è così a livello fisico.
livello di trasporto: processi che parlano tra di loro che si basa sui servizi del livello di rete e fornisce servizi al livello applicazione.

>[!note] Indirizzamento
>C'è bisogno di un indirizzamento perché sullo stesso host possono esserci più processi. 
>Abbiamo bisogno di un indirizzo IP del client e del server, indirizzo di processo dell'host e del server

>[!warning] Indirizzo IP vs porta
>porta = indirizzo a livello di trasporto
>IP = indirizzo a livello di rete
>IP + porta = *socket di rete*

Ovviamente poiché ci possono essere più processi e più messaggi da essi, avviene un processo di multiplexing/demultiplexing (i pacchetti vengono gestiti uno alla volta).
>[!note] Socket API
>Un'API che ci permette di gestire pacchetti di trasporto.
>Un socket appare come un punto di ingresso o di uscita, è una struttra dati utilizzata dal processo applicativo (socket client e socket server). Contiene **indirizzo IP e numero di porta**. I numeri di porta hanno 16 bit e i primi 1024 sono *well known*.
>L'interazione tra client e server è bidirezionale, è necessaria quindi una coppia di socket (*locale e mittente*). 
>Il client ha bisogno di un socket locale e uno remoto per comunicare.
>**Socket locale**
>- IP è noto
>- La porta viene assegnata in modo temporaneo, non deve essere utilizzato da altri processi in quel momento (*porta effimera*)
>socket remoto
>- Il numero di porta è noto in base all'applicazione
>- L'IP è fornito dal DNS
>- Oppure entrambi definiti dal programmatore
>
> Anche lato server deve individuare i socket
> - IP locale noto
> - Porta nota assegnata dal progettista
> socket remoto
> - All'interno della richieste ci sono le informazioni riguardo l'IP e la porta
>
>>[!warning] Il socket address locale di un server non cambia mai, mentre quello remoto varia ad ogni interazione con client diversi

## Servizi di trasporto
- Affidabile -> TCP
- Non affidabile -> UDP
>[!note] TCP
>Viene definito orientato alla connessione, tramite uno scambio di messaggi tra client e server si crea una "connessione".
>Il trasporto è affidabile tra processi di invio e di ricezione. C'è un controllo di flusso per non sovraccaricare il destinatario, mentre il controllo della congestione si allarga a più nodi della rete (è una caratteristica della rete) è quindi un problema intermedio tra mittente e destinatario.
>Questo servizio però non offre garanzie sulla temporizzazione, ampiezza di banda e sicurezza(per quest'ultima c'è bisogno di ulteriori protocolli).

>[!note] UDP
>Non è prevista una connessione, nessun setup tra client e server, questo redne il trasferimento dati tra processi inaffidabile, senza i controlli e le garanzie di UDP.

## UDP User Datagram Protocol
Protocollo di trasporto inaffidabile e privo di connessione. 
Fornisce servizi di:
- comunicazione
- multiplexing/demultiplexing
- incapsulamento/decapsulamento
L'unico controllo è quello di correttezza sul singolo pacchett (**checksum**).
>[!tip] Servizio connectionless
>Ogni pacchetto è indipendente dll'altro, l'ordine di arrivo può essere diverso da quello di spedizione. Non c'è coordinazione tra liello trasporto mittente e destinatario.

Rappresentazione tramite FSM ( )
