# Indirizzi MAC
Sono associati alla scheda di rete dal produttore, è un indirizzo univoco.
Questi indirizzi presenti nell'intestazione cambiano ogni volta che il frame raggiunge un nodo diverso.
Anche nel caso di indirizzi MAC abbiamo l'indirizzo broadcast: **FF-FF-FF-FF**.
pipo
### Protocollo ARP
Serve per determinare l'indirizzo MAC di un nodo partendo dall'IP. Ogni nodo ha una tabella ARP al proprio interno che mantiene l'associazione tra indirizzi IP e MAC man mano che li scopre (queste informazioni hanno un time to live temporaneo per non avere troppe informazioni da memorizzare).

# Indirizzamento
A livello fisico non c'è indirizzamento come negli altri livelli dello stack protocollare.
