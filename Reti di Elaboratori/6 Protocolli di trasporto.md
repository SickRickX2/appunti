Siamo al livello di trasporto, 
Protocolli di trasporto forniscono la *comunicazione logica* tra processi applicativi di host differenti. Come se fossero connessi direttamente anche se non è così a livello fisico.
**Livello di trasporto**: *comunicazione tra processi*, processi che parlano tra di loro che si basa sui servizi del livello di rete e fornisce servizi al livello applicazione.
**Livello di rete**: *comunicazione tra host*, si basa sui servizi del livello di collegamento

>[!note] Indirizzamento
>C'è bisogno di un indirizzamento perché sullo stesso host possono esserci più processi. 
>La maggior parte dei sistemi operativi è multiutente e multiprocesso.
>Per stabilire una comunicazione tra i due processi è necessario un metodo per individuare:
>- Host locale
>- Host remoto 
>- Processo locale
>- Processo remoto
>
>In sostanza abbiamo bisogno di un indirizzo IP del client e del server, indirizzo di processo dell'host e del server

>[!warning] Indirizzo IP vs porta
>porta = indirizzo a livello di trasporto
>IP = indirizzo a livello di rete
>IP + porta = *socket di rete*

Ovviamente poiché ci possono essere più processi e più messaggi da essi, avviene un processo di multiplexing/demultiplexing (i pacchetti però vengono gestiti uno alla volta).

>[!danger] Nota bene
>- *Numero di porta*: identifica il processo applicativo
>- *Indirizzo IP destinatario*: identifica il server (host)

>[!note] Socket API
>Un'API che ci permette di gestire pacchetti di trasporto.
>Un **socket** appare come un punto di ingresso o di uscita, è una **struttra dati** utilizzata dal processo applicativo (*socket client e socket server*). Contiene **indirizzo IP e numero di porta**. I numeri di porta hanno 16 bit e i primi 1024 sono *well known* e già assegnati.
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

>[!note] Multiplexing e Demultiplexing
>>[!example] Esempio dei condomini
>>I portieri effettuano un'operazione di 
>>- *Multiplexing* quando raccolgono le lettere dai condomini (mittenti) e le imbucano
>>- *Demultiplexing* quando ricevono le lettere dal postino, leggono il nome riportato su ciascuna busta e consegnano ciascuna lettera al rispettivo destinatario
>
>**Come funziona il demultiplexing**
>*L'host riceve i datagrammi IP* 
>- ogni datagramma ha un indirizzo IP di origine e di destinazione
>- ogni datagramma trasporta 1 segmento a livello di trasporto
>- ogni segmento ha un numero di porta di origine e un umero di destinazione
>
>*L'host usa gli indirizzi IP e i numeri di porta per inviare il segmento al processo appropriato*
>![[Pasted image 20250321101158.png|350]]
>
>
## Servizi di trasporto
- Affidabile -> TCP
- Non affidabile -> UDP

>[!note] TCP
>Viene definito **orientato alla connessione**, tramite uno scambio di messaggi tra client e server si crea una "*connessione*".
>Il trasporto è affidabile tra processi di invio e di ricezione. C'è un controllo di flusso per non sovraccaricare il destinatario, mentre il controllo della congestione si allarga a più nodi della rete (è una caratteristica della rete) è quindi un problema intermedio tra mittente e destinatario.
>Questo servizio però non offre garanzie sulla temporizzazione, ampiezza di banda e sicurezza(per quest'ultima c'è bisogno di ulteriori protocolli).

>[!note] UDP
>Non è prevista una connessione, nessun setup tra client e server, questo rende il trasferimento dati tra processi inaffidabile, senza i controlli e le garanzie di TCP.

# UDP User Datagram Protocol
Protocollo di trasporto inaffidabile e privo di connessione. 
Fornisce servizi di:
- comunicazione
- multiplexing/demultiplexing
- incapsulamento/decapsulamento
L'unico controllo è quello di correttezza sul singolo pacchetto (**checksum**).

![[Pasted image 20250321102302.png|500]]

>[!tip] Servizio connectionless
>Ogni pacchetto è *indipendente* dall'altro, l'ordine di arrivo può essere diverso da quello di spedizione. Non c'è coordinazione tra livello trasporto mittente e destinatario.

#### Rappresentazione tramite FSM ( Finite State Machine)
Il comportamento di un protocollo di trasporto può essere rappresentato da un automa a stati finiti. L'automa rimane in uno stato fin quando non avviene un evento che può modificare lo stato dell'automa e fargli compiere un'azione.
![[Pasted image 20250321102506.png]]
>[!note] Datagrammi UDP
>Non vi è alcun flusso di dati, il processo mittente non può inviare un flusso di dati e aspettarsi che UDP lo suddivida in datagrammi correlati.
I pacchetti devono inviare richieste di dimensioni sufficientemente piccole per essere inserite ciascuna in un singolo datagramma utente.

>[!tip] Checksum
>Controlla se ci sono state interferenze sovrapposte alla trasmissione del pacchetto. 
>Per fare questo controllo:
>- il messaggio viene diviso in parole da 16 bit
>- il valore checksum viene impostato a 0
>- tutte le parole del messaggio vengono

>[!tip] DNS usa UDP
Quando vuole effettuare una query la passa a UDP, perché è un protocollo molto semplice e veloce 

# TCP
Non abbiamo proprio pacchetti ma un flusso di byte continuo, l'ordine delle informazione vien preservato.
Servizi del TCP:
- Trasporto orientato della connession
- le altre cose...
>[!note] Demultiplexing orientato alla connessione
>I socket sono identificati da 4 parametri
>L'host ricevente usa i quattro parametri per inviare il segmento alla socket appropriata. Si possono usare più socket contemporaneamente.
>>[!warning] Sulla stessa porta possono essere attive più socket

>[!tip] Servizio connection oriented
>Servizio end-to-end.
>Il destinatario deve essere in grado di riordinare i dati del pacchetto. Per fare ciò c'è bisogno di stabilire una connessione.

### Rappresentazione tramite FSM

>[!note] Controllo di flusso
>Deve esserci equilibrio tra velocità di produzione e velocità di consumo di dati.
>Serve per non sovraccaricare il consumatore, processo destinatario.
>- *Buffer* sono locazioni di memoria che possono contenere pacchetti e la comunicazione di informazioni di flusso può avvenire tramite segnali dal consumatore al produttore. 

>[!note] Controllo dei problemi
>- Rilevare e scartare pacchetti corrotti
>- Tenere traccia dei pacchetti persi e gestirne il rinvio
>- Riconoscere pacchetti duplicati e scartarli
>- Bufferizzare i pacchetti fuori sequenza 
>
>Abbiamo bisogno di una numerazione dei pacchetti : *numero di sequenza*, poiché il numero di sequenza deve essere inserito nell'intestazione del pacchetto occore specificarne la dimensione massima.
>Questo numero è utile al destinatario per capire la sequenza di arrivo, pacchetti persi e pacchetti duplicati.
>Per far capire al mittente che si è perso un pacchetto abbiamo bisogno di un *numero di riscontro*.

>[!note] Controllo della congestione
>Avviene quando vengono spediti troppi pacchetti in rete, superiore alla possibilità di gestione della rete.



