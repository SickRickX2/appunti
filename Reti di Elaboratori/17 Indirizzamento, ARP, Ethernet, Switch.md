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

>[!tip] CSMA/CD
>*Framing*