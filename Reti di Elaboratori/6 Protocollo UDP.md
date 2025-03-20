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
- 