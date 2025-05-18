- **LAN wireless**
	- Disponibili in campus universitari, uffici, bar aree pubbliche
- **Reti cellulari**
	- Il numero di abbonati alla telefonia mobile supera quello della telefonia fissa
- **Bluetooth**
- **Reti di sensori, RFID, smart objects**

![[Pasted image 20250518191830.png]]
**Base station**
![[Pasted image 20250518191956.png]]
tipicamente connessi alla rete cablata, responsabile di mandare i pacchetti tra le reti cablate e le reti wireless
**Wireless link**
![[Pasted image 20250518192132.png]]
Tipicamente usato per connettere i dispositivi mobili alla base station, anche usato come collegamento backbone, protocolli ad accessi multipli coordinano i link access.

### Caratteristiche LAN wireless
**Mezzo trasmissivo**: aria, segnale broadcast, mezzo condiviso dagli host della rete
**Host wireless**: non è fisicamente connesso alla rete e può muoversi liberamente
**Connessione ad altre reti**: mediante una stazione base detta *Access Point (AP)* che unisce l'ambiente wireless all'ambiente cablato.
![[Pasted image 20250518192742.png]]

>[!note] Migrazione dall'ambiente cablato al wireless
>Il funzionamento di una rete cablata o wireless dipende dai due sottolivelli inferiori dello stack protocollare (**collegamento e fisico**).
>Per **migrare** dalla rete cablata a quella wireless è *sufficiente cambiare le schede di rete e sostituire lo switch di collegamento con un AP*.
>- Gli indirizzi MAC cambiano mentre gli IP rimangono gli stessi.

### Reti ad hoc (senza infrastruttura)
Insieme di host che si auto-organizzano per formare una rete e comunicano liberamente tra di loro.
- Ogni host deve eseguire le funzionalità di rete quali network setup, routing, forwarding etc.
![[Pasted image 20250518193655.png|300]]

### Caratteristiche del link wireless
- **Attenuazione del segnale**: la forza dei segnali elettromagnetici diminuisce rapidamente all'aumentare della distanza dal trasmettitore in quanto il segnale si disperde in tutte le direzioni![[Pasted image 20250518193913.png|300]]
- **Propagazione multii-path**: Quando un'onda radio trova un ostacolo, tutta o una parte dell'onda è rifelssa, con una perdita di potenza. Un segnale sorgente può arrivare, tramite riflessi successivi, a raggiungere una stazione o un punto di accesso attraverso percorsi multipli.

- **Interfereze**:
	- dalla stessa sorgente: un destinatario può ricevere più segnali dal mittente desiderato a *causa del multipath*
	- da altre sorgenti: altri trasmettitori stanno usando la *stessa banda di frequenza* per comunicare con altri destinatari

#### Errori
Le caratteristiche dei link wireless causano errori. *Signal to Noise Ratio (SNR)* o rapporto segnale-rumore misura il rapporto tra il segnale buono e quello cattivo (segnale contro rumore).
- *Alto*: il segnale è più forte del rumore, quindi può essere convertito in dati reali
- *Basso*: il segnale è stato danneggiato dal rumore e i dati non possono essere recuperati

