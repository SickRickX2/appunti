Si occupa del trasferimento dei datagrammi nel momento incui abbiamo un host mittente e un host destinatario.
Funzioni chiave:
- *Instradamento (routing)*: determina il percorso seguito dai pacchetti dall'origine alla destinazione (la strada che deve fare il pacchetto per arrivare a destinazione).
- *Inoltro(forwarding)*: trasferisce i paccchetti dall'input del router all'output del router appropriato.

Ogni router ha la propria tabella di routing.

### Switch e Router
Un router è uno switch ma con funzionalità diverse.
>[!note] Switch
>Si occupa del trasferimento dall'interfaccia di input all'interfaccia di output.

- **Link Layer Switch** se l'inoltro avviene in relazione al valore del campo nel livello di collegamento (livello 2)
- **Router** se l'inoltro avviene in relazione al valore del campo nel livello di rete (livello 3)

>[!note] Link Layer Switch
>Utilizzato per collegare i singoli computer all'interno di una rete LAN

### Switching
>[!note] Approccio a circuito virtuale
>I due sistemi terminali instaurano prima una connessione (servizio orientato alla connessione)
>
>Viene utilizzata un'etichetta di circuito all'interno della tabella per indicare l'interfaccia di uscita e la virtual circuit d'uscita.

>[!note] Reti a datagramma
>Internet è una rete ad anagramma.

## Router
Implementa i primi tre livelli, all'interno abbiamo:
- *porte di input*: livello fisico e collegamento
- *porte di output*: livello fisico e collegamento
- *Switching Fabric*: livello di rete, è una struttura di commutazione che permette ad un datagramma in entrata a commutare ad una porta d'uscita
- *Processore di Routing*: cerca la riga corretta nella table lookup per trovare l'interfaccia di uscita

>[!tip] Ricerca nella tabella di inoltro
>Il modo migliore è quello di seguire una struttura ad albero, si parte dalla radice e si va a sinistra o a destra se il bite è 0 o 1.

>[!note] Commutazione tramite bus
>C'è un bus condiviso in cui transitano i pacchetti dalle porte di ingresso, ma si può inviare solo un pacchetto alla volta

>[!note] Commutazione attraverso rete d'interconnessione
>In questo caso abbiamo una rete d'interconnessione composta da 2n bus, questo permette di inviare più pacchetti in contemporanea

>[!note] Porte d'uscita

>[!tip] Accodamento
>Dipende dalla velocità di commutazione e dalla congestione sulle porte

# Protocollli del livello di rete
- IP:
- IGMP:
- ICMP:
- ARP: mantiene l'associazione tra l'indirizzo ip e l'indirizzo mac
- DHCP: assegna ad un host un indirizzo ip in maniera dinamica

## Internet Protocol (IPv4)
Responsabile della suddivisione in pacchetti, dell'inoltro (forwarding), e della consegna dei datagrammi al livello di rete (host ot host), è un protocollo inaffidabile, senza connessione e basato su datagrammi.