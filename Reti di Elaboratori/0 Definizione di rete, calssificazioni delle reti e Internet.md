>[!note] Info
>Prof.ssa Gaia Maselli
>maselli@di.uniroma1.it
>codice classroom: 27vt4xu
>**Materia:** [[Reti degli Elaboratori (class)]]
# Le reti
Una rete è composta da dispositivi in grado di *scambiarsi informazioni*, quali **sistemi** **terminali** e **dispositivi di interconnessione**. 

I **nodi** sono una componente della rete, collegati tra loro tramite i **link** che permettono la comunicazione. Ci sono nodi in cui girano le app (*Host* o *Server*) e nodi intermedi  che si occupano di far viaggiare i dati(*Router* o *Switch*).

>[!note] Sistemi terminali
>- **Host**: macchine in genere di proprietà dell'utente che ospitano le applicazioni
>- **Server**: molto più potenti dell'host destinato ad eseguire programmi che forniscono servizio alle applicazioni utente. Tipicamente gestiti dagli amministratori di sistema

>[!note] Dispositivi di interconnessione
>- **Router**: collegano una rete ad un'altra
> - **Switch**: sono all'interno di una rete e collegano sistemi terminali tra di loro
>- **Modem**: trasformano i dati digitali in dati analogici e viceversa

>[!note] Collegamenti
>- **cablati o guidati**: rame o fibra ottica
>- **wireless**: onde elettromagnetiche o satellite

**bit**: viaggia da un sistema terminale ad un altro

Mezzi trasmissivi cablati:
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
![[Pasted image 20250227230557.png]]

## Reti LAN: Local Area Network
Solitamente una **rete privata** che collega i sistemi terminali in un singolo ufficio (azienda, università). Ogni sistema ha un indirizzo IP e non c'è un numero specifico minimo o massimo di dispositivi
Nasce con lo scopo di condivider risorse tra sistemi terminali che ne facevano parte, in seguito è stata estesa ad altre lan o wan:

### LAN con cavo condiviso
Il pacchetto inviato ad un dispositivo viene ricevuto da tutti gli altri tramite un singolo cavo, viene chiamata rete **broadcast**; solo il desinatario elabora il pacchetto mentre tutti gli altri lo ignorano. La regola è che può trasmettere un solo nodo alla volta, altrimenti si crea una collisione
![[Pasted image 20250227230836.png]]

### LAN con Switch
Ogni nodo è direttamente collegato allo switch. Lo switch è in grado di riconoscere chi sta trasmettendo e capisce come distribuire i dati per la comunicazione lavorando sugli indirizzi dei nodi. A ricevere le informazioni è solo lo switch e non tutti i terminali insieme. Questo permette una comunicazione parallela.
![[Pasted image 20250227231304.png]]

## Le reti WAN: Wide Area Network
Rete geografica, interconnessione di dispositivi che può servire una città, regione o nazione. Questa rete non interconnette host ma switch, router e modem e viene gestita da un operatore di telecomunicazioni (*Internet Service Provider- ISP*):
 >[!note]  WAN Punto-punto
> Collega due mezzi di comunicazione tramite un mezzo trasmissivo (cavo o rete wireless)
> ![[Pasted image 20250228093618.png]]

>[!note] WAN a commutazione
>Rete con più di due punti di terminazione, viene utilizzata nelle dorsali di Internet
>![[Pasted image 20250228093746.png]]
## Internetwork 
Oggigiorno è difficile trovare LAN o WAN isolate: esse sono in genere connesse fra di loro per formare una internetwork, o internet
>[!example] Internetwork composta da due LAN e una WAN punot-punto
>![[Pasted image 20250228094130.png]]
>esempio: un'azienda ha due uffici in due città differenti. In Ciascun ufficio esiste una LAN che consente agli impiegati di comunicare tra di loro. Per mettere in comunicazione le due LAN l'azienda affitta un'apposita WAN punto-punto da un ISP, realizzando una internetwork o internet privata. Il compito dei router è quello di instradare i pacchetti da una LAN all'altra.

>[!example] Rete eterogenea
>Se si vuole creare una WAN più estesa in base alle proprie necessità si può fare usando diverse combinazioni. Un esempio composta da quattro WAN e tre LAN:
>![[Pasted image 20250228094724.png]]
## Rete GARR 
La rerte GARR collega luoghi di cultura e ha un'infrastruttura molto potente tra collegamenti in dorsale (100 Gbps) e di accesso (40 Gbps). 
# Commutazione (switching)
Una *internet* (internetwork) è una combinazione di link e dispositivi capaci di scambiarsi informazioni. In particolare i sistemi terminali appartenenti alla rete comunicano tra di loro per mezzo di dispositivi come **switch** e **router** che si trovano tra sistemi terminali.
In base al funzionamento possiamo avere due tipi di reti:
## 1) Reti a commutazione di circuito
Viene sempre stabilito un collegamento dedicato tra due dispositivi denominato **circuito**, dove viaggeranno tutte le informazioni fino a termine della comunicazione. Vengono riservate le risorse necessarie per l'intera durata della comunicazione, queste informazioni vengono mantenute dalla rete. Non è flessibile in termini di gestione di risorse.
![[Pasted image 20250228100339.png]]
La banda può essere allocata in modi diversi:
- **Divisione su frequenza (FDM)**: lo spettro viene diviso in sottointervalli, in cui ogni sottointervallo può trasmettere consecutivamente ma con le risorse statiche
- **Divisione temporale (TDM)**: dò tutte le risorse ad intervalli piccolissimi in maniera ciclica ad ogni utente

## 2) Reti a commutazione di pacchetto (Store and Forward)
Internet funziona in questo modo oggi, in questo caso non viene riservata alcun tipo di risorsa ma vengono suddivisi i dati in vlocchi di *pacchetti*.
In questo caso la trasmissione non avviene in maniera continua ma c'è una **coda** all'interno del router per la spedizione dei pacchetti (indipendenti tra loro). Ogni router riceve il pacchetto, lo memorizza e lo inoltra al terminale di destinazione. 
Ci sono **code di ingresso e code di uscita**.
![[Pasted image 20250228100837.png]]

# Internet
L'internet più famosa è chiamata **Internet** ed è composta da migliaia di reti interconnesse, è una rete a commutazione di pacchetto.
>[!tip]  Rappresentazione concettuale di Internet
>![[Pasted image 20250228101739.png]]
### L'accesso a internet
L'Internet è una internetwork che concsente a qualsiasi utente di farne parte.
L'utente, tuttavia, deve essere fisicamente collegato a un ISP , solitamente mediante una WAN punto-punto.
Il collegamento che connette l'utente al primo router di Internet è detto **rete di accesso**.
L'accesso può avvenire tramite:
- Rete telefonica: 
	- DSL
	- Servizio dial-up
- Reti wireless: 
	 - Wi-Fi
	 - Cellulare
- Collegamento diretto:
	- aziende di grandi dimensioni possono avere ISP locali, affittando delle reti WAN da un operatore.

### Accesso via rete telefonica
Si collega modificando la linea telefonica fra la sede del dispositivo che vuole connettersi e la centrale telefonica con una WAN punto-punto.
Limiti:
- lentezza
- impossibilità di parlare e navigare contemporaneamente
Il servizio **DSL** ha semplicemente un filtro per il collegamento tra ISP e abitazione, più veloce e permette di utilizzare voce e dati.

### Accesso tramite Ethernet
Un metodo di accesso molto affidabile e veloce. Lo switch (Ethernet) della LAN è generalmente collegato a un router che è connesso ai router della dorsale.
### Accesso wireless
- Wi-Fi: Ci si collega tramite accesspoint collegato alla rete cablata
 - Cellulare: si usa la rete cellulare, acces point della compagnia telefonica cellulare con raggio di azione di decine di kilometri

