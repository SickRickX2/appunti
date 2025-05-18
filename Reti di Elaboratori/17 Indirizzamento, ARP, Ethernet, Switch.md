# Indirizzi MAC
Sono associati alla scheda di rete dal produttore, è un indirizzo univoco a 48 bit (6 byte rappresentati in esadecimale).

Questi indirizzi presenti nell'intestazione cambiano ogni volta che il frame raggiunge un nodo diverso.

Anche nel caso di indirizzi MAC abbiamo l'indirizzo broadcast: **FF-FF-FF-FF-FF-FF**.
### Protocollo per la risoluzione degli indirizzi (ARP)

Serve per determinare l'indirizzo MAC di un nodo partendo dall'IP. 
Ogni nodo ha una tabella ARP al proprio interno che mantiene l'associazione tra indirizzi *IP e MAC* man mano che li scopre (queste informazioni hanno un time to live temporaneo per non avere troppe informazioni da memorizzare).

# Indirizzamento

A livello fisico non c'è indirizzamento come negli altri livelli dello stack protocollare, questo livello si occupa di trasferire i singoli bit in broadcast nel mezzo trasmissivo e ricevuti da tutti i nodi che sono collegati.

## Protocollo ETHERNET
Fu implementato dalla IEEE computer society nel 1985 per definire le funzioi del livello fisico e dei protocolli LAN.

>[!note] Protocollo IEEE 802
>I vari standard differiscono a livello fisico e nel sottolivello MAC.

La specifica del protocollo Ethernet si è sempre adattata anche con il miglioramento delle tecnologie. Infatti i vari standard differiscono a livello fisico e nel sottolivello MAC, ma sono compatibili a livello data link.

>[!note] Ethernet
>Detiene una posizione dominante nel mercato delle LAN cablate.
>- è stata la prima LAN ad alta velocità con vasta diffusione
>- più semplice e meno costosa di token ring, FDDI, ATM
>- sempre al passo dei tempi con il tasso trasmissivo

### Ethernet STANDARD (10 Mbps)
![[Pasted image 20250513121442.png]]

**Formato dei frame**
![[Pasted image 20250513121526.png]]
- *Preambolo* 7 byte
	- 7 byte hanno i bit 10101010
	- serve per **attivare** le "**NIC**" dei riceventi e sincronizzare i loro orologi con quello del trasmittente
	- fa parte dell'header del livello fisico
- *SFD (Start Frame Delimeter)*: 1 byte (10101011)
	- flag che definisce l'inizio del frame (ultima possibilità di sincronizzazione)
	- gli ultimi due bit "11" indicano che inizia l'header MAC
- *Indirizzi sorgente e destinazione*: 6 byte
	- quando una NIC riceve un pacchetto contenente il proprio indirizzo di destinazione o l'indirizzo broadcast, trasferisce il contenuto del campo dati del pacchetto al livello di rete
	- i pacchetti con altri indirizzi MAC vengono ignorati
- *Tipo*: 2 byte per **multiplexing/demultiplexing** 
- *Dati*:contiene datagramma di rete. Se il datagramma è inferiore alla dimensione minima il campo viene **stuffed** con degli zeri fino a raggiungere quel valore
- *CRC*: consente alla NIC ricevente di rilevare la presenza di un errore nei bit sui campi indirizzo, tipo e dati

Questo quindi è un protocollo:
*senza connessione*, non è prevista nessuna forma di handshake preventiva con il destinatario prima di inviare un pacchetto.
*non affidabile (come IP e UDP)*: la NIC ricevente non invia un riscontro

**Indirizzi**
Tutte le stazioni che fanno parte di una ethernet sono dotate di una **Network Interface Card**(NIC) o scheda di rete.
La NIC fornisce un indirizzo di rete di livello di collegamento. Gli indirizzi vengono trasmessi da sinistra verso destra, byte per byte, ma per ciascun byte il bit meno significativo viene inviato per primo e quello più significativo per ultimo.

>[!tip] Fasi operative del protocollo CSMA/CD
>1) *Framing*: La NIC riceve un datagramma di rete dal nodo cui è collegato  e prepara un frame Ethernet.
>2) *Carrier Sense e trasmissione*: Se il canale è inattivo (misura il livello di energia sul mezzo trasmissivo per un breve periodo di tempo) inizia la trasmissione. Se il canale risulta occupato, resta in attesa fino a quando non rileva più il segnale, a quel punto trasmette.
>3) *Collision detection*: Verifica durante la trasmissione, la presenza di eventuali segnali provenienti da altre NIC. Se non ne rileva, considera il pacchetto spedito.
>4) *Jamming*: Se rileva segnali da altre NIC, interrompe immediatamente la trasmissione del pacchetto e invia un segnale di disturbo (jam di 48 bit)
>5) *Backoff esponenziale*: la NIC rimane in attesa. Quando riscontra l'n-esima collisone consevutiva stabilisce un valore k tra $\{0,1,2,..., 2^{m-1}\}$, dove $m$ è il minimo tra $n$ e $10$. La NIC aspetta un tempo pari a $K$ volte $512$ bit e ritorna al passo 2
>

### Fast Ethernet (100Mbps)
La standard si evolve in fast, mantenendo la compatibilità con la versione precedente.
- Il sottolivello MAC rimane invariato, compreso il formato del frame e le sue dimensioni.
- Problemi con funzionamento di CSMA/CD?

>[!tip] Metodo di accesso Fast Ethernet
>Il funzionamento corretto del CSMA/CD dipende dallavelocità di trrasmissione, dalla dimensione minima del frame e dalla lunghezza massima della rete.
>Se si vuole mantenere la dimensione minima del frame a 512 bit allora bisogna modificare la lunghezza massima della rete.
>- Se la trasmissione è 10 volte più veloce e il frame è ancora di 512 bit, allora le collisioni devono essere rilevate 10 volte più velocemente, quindi la rete dovrebbe essere 10 volte più corta.

#### Prima soluzione
Abbandonare la vecchia tipologia in linea per una tipologia a stella, utilizzare un hub e fissare la lunghezza della rete da 2500 metri a 250.
![[Pasted image 20250518173347.png|450]]

L'**hub** (ripetitore a multiporta)è un dispositivo che opera sui singoli bit:
- opera a *livello fisico*
- all'arrivo di un bit, l'hub lo riproduce incrementandone l'energia e lo trasmette attraverso tutte le sue altre interfacce
- non implementa la rilevazione della portante né CSMA/CD 
- ripete il bit entrante su tutte le interfacce uscenti anche se su qualcuna di queste c'è un segnale
- trasmette in broadcast, e quindi ciascuna NIC può sondare il canale per verificare se è libero e rilevare una collisione mentre trasmette
#### Seconda soluzione
Si usa uno **switch** di collegamento *dotato di buffer* per memorizzare i frame e *connessione full duplex* per ciascun host. Il mezzo trasmissivo è privato per ciascun host e non c'è bisogno di usare CSMA/CD dal momento che gli host non sono più in competizione.
Lo switch riceve un frame da un host, lo memorizza nel buffer, verifica l'indirizzo di destinazione e invia il frame attraverso l'interfaccia corrispondente.
Il singolo mezzo condiviso è stato modificato in molti mezzi punto-punto.

>[!note] Switch
>Dispositivo del livello di link: più intelligente di un hub. svolge un ruolo attivo.
>- Opera a *livello di collegamento*
>- Filtra e inoltra i pacchetti Ethernet
>- Esamina l'indirizzo di destinazione e lo invia all'interfaccia corrispondente alla sua destinazione.
>
>*Trasparente*: Gli host non sono consapevoli della presenza dello switch
>
>Consente più trasmissioni simultanee, gli host hanno collegamenti dedicati e diretti con lo switch. Il protocollo ethernet è usato su ciascun collegamento in entrata, ma non si verificano collisioni; full duplex.
>*switching*: da A ad A' e da B a B' simultaneamente, senza collisioni
>![[Pasted image 20250518182641.png]]


## Gigabit Ethernet
Successiva  versione di Ethernet a 1000 Mbps. Topologia a stella con switch, no collisioni (la massima lunghezza del cavo dipende solo dall'attenuazione del segnale).

**Switch: apprendimento** 
Inizialmente gli switch venivano configurati staticamente, ora c'è un meccanismo dinamico di auto-apprendimento:
- non hanno bisogno di essere configurati
- una tabella dinamica associa automaticamente gli indirizzi MAC alle porte (interfacce)

Lo switch *apprende* quali nodi possono essere raggiunti attraverso determinate interfacce
- quando riceve un pacchetto, lo switch "impara" l'indirizzo del mittente 
- registra la coppia mittente/interfaccia nella sua tabella di commutazione

# VLAN
Rete locale configurata per mezzo del software anziché del cablaggio fisico.
La LAN viene suddivisa in segmenti logici anziché fisici, una LAN può essere suddivisa in più VLAN. Il gruppo di appartenenza è definito dal software.
![[Pasted image 20250518184131.png]]
Il maagement software dello switch permette all'amministratore di rete di dichiarare  quali porte apprtengono a una data LAN. Lo switch mantiene una tabella di associazioni porta VLAN.

Si può anche creare un'unica LAN su più switch
