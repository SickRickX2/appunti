>[!note] Info
>Prof.ssa Gaia Maselli
>maselli@di.uniroma1.it
>codice classroom: 27vt4xu

I nodi sono una componente della rete, collegati tra loro tramite i link che permettono la comunicazione tra di loro. Ci sono nodi in cui girano le app (HOST o SERVER) e nodi intermedi  che si occupano di far viaggiare i dati(router o switch).
Una rete è composta da dispositivi in grado di scambiarsi informazioni (sistemi terminali) e sistemi che fanno viaggiare i dati (dispositivi di interconnessione)

*Sistemi terminali:*
- **host**: macchine in genere di proprietà dell'utente che ospitano le applicazioni
- **server**: molto più potenti dell'host e forniscono servizio alle applicazioni utente. Tipicamente gestiti dagli amministratori di sistema

*Dispositivi di interconnessione:*
- **Router**: collegano una rete ad un'altra
- **Switch**: sono all'interno di una rete e collegano sistemi terminali tra di loro
- **Modem**: trasformano i dati digitali in dati analogici e viceversa

*Collegamenti*:
- **cablati o guidati**: rame o fibra ottica
- **wireless**: onde elettromagnetiche o satellite

Mezzi trasmissivi cablati:
- **bit**: viaggia da un sistema terminale ad un altro
- mezzo fisico: che sta tra il trasmittente e il ricevente
- Fibra ottica: viaggiano impulsi di luce e non subisce interferenze, il che riduce il tasso di errrore

Mezzi trasmissivi wireless:
non richiedon installazione fisica di cavi, sono bidirezionali ma soffrono molto l'ambiente circostante a causa di:
- riflessione
- ostruzione da parte di ostacoli
- interferenza

canali radio:
- LAN
- wide-area
- satellitari

## Classificazione delle reti
mettere tabella

## Reti LAN: Local Area Network
Solitamente una rete privata che collega i sistemi terminali in un singolo ufficio (azienda, università). Ogni sistema ha un indirizzo IP e non c'è un numero specifico minimo o massimo di dispositivi
Nasce con lo scopo di condivider risorse tra sistemi terminali che ne facevano parte, in seguito è stata estesa ad altre lan o wan:

### LAN con cavo condiviso
Il pacchetto inviato ad un dispositivo viene ricevuto da tutti gli altri tramite un singolo cavo, viene chiamata rete **broadcast**; solo il desinatario elabora il pacchetto mentre tutti gli altri lo ignorano. La regola è che può trasmettere un solo nodo alla volta, altrimenti si crea una collisione

### LAN con Switch
Ogni nodo è direttamente collegato allo switch. Lo switch è in grado di riconoscere chi sta trasmettendo e capisce come distribuire i dati per la comunicazione lavorando sugli indirizzi dei nodi. A ricevere le informazioni è solo lo switch e non tutti i terminali insieme. Questo permette una comunicazione parallela.

## Le reti WAN
Rete geografica che può servire una città, regione o nazione. Questa rete non interconnette host ma switch, router e modem e viene. gestita da un operatore di telecomunicazioni:
- WAN punto-punto: collega due mezzi
- WAN a coomutazione: collega più dispositivi e viene utilizzzata nelle dorsali di internet

## Internetwork 
Essa è composta da due LAN e due WAN punto-punto per una rete privata altrimenti si utilizza una wan più estesa. In base alle necessità si possono fare diverse tipe di combinazioni
## Rete GARR 
La rerte GARR collega luoghi di cultura e ha un'infrastruttura molto potente tra collegamenti in dorsale (100 Gbps) e di accesso (40 Gbps). 

# Commutazione (switching)
Una internet è una combinazione di link e dispositivi capaci di scambiarsi informazioni. In particolare i sistemi terminali appartenenti alla rete comunicano tra di loro per mezzo di dispositivi come switch e router che si trovano tra sistemi terminali.
In base al funzionamento possiamo avere due tipi di reti:
## Reti a commutazione di circuito
Viene stabilito un collegamento dedicato tra due dispositivi denominato **circuito**, dove viaggeranno tutte le informazioni fino a termine della comunicazione. Vengono riservate le risorse necessarie per la comunicazione, queste informazioni vengono mantenute dalla rete.

## Reti
