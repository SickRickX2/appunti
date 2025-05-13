# Indirizzi MAC
Sono associati alla scheda di rete dal produttore, è un indirizzo univoco a 48 bit (6 byte rappresentati in esadecimale).

Questi indirizzi presenti nell'intestazione cambiano ogni volta che il frame raggiunge un nodo diverso.
Anche nel caso di indirizzi MAC abbiamo l'indirizzo broadcast: **FF-FF-FF-FF**.
pipo
### Protocollo ARP
Serve per determinare l'indirizzo MAC di un nodo partendo dall'IP. Ogni nodo ha una tabella ARP al proprio interno che mantiene l'associazione tra indirizzi IP e MAC man mano che li scopre (queste informazioni hanno un time to live temporaneo per non avere troppe informazioni da memorizzare).

# Indirizzamento
A livello fisico non c'è indirizzamento come negli altri livelli dello stack protocollare.

## Protocollo ETHERNET
Fu implementato dalla IEEE computer society nel 1985 per definire le funzioi del livello fisico e dei protocolli LAN.
>[!note] Protocollo IEEE 802
>I vari standard differiscono a livello fisico e nel sottolivello MAC.

La specifica del protocollo Ethernet si è sempre adattata anche con il miglioramento delle tecnologie.

