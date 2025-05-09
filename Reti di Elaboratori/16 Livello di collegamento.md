Andremo a vedere la comunicazione nel collegamento *hop-to-hop* o *nodo-a-nodo*.
Host e router vengono definiti come nodi o *stazioni*, mentre i collegamenti possono essere cablati o wireless.

I collegamenti possono essere di due tipi
- **punto-punto** collegamento dedicato solo a due dispositivi
- **broadcast**: collegamento condiviso da più dispositivi

>[!note] Servizi offerti
>*Framing*: incapsulamento, aggiunta dell'intestazione al datagramma (si passa da datagramma a frame). Per identificare origine e destinatario vengono utilizzati indirizzi "**MAC**"
>*Consegna affidabile*: non tutti ma la maggior parte, grazie all'utilizzo di ack.
>*Controllo di flusso*: si cerca di evitare di sovraccaricae il destinatario
>*Controllo degli errori*: di solito causato dalle **interferenze** a causa di segnali che si sovrappongono.
>*Correzione degli errori*: non li vediamo ma ci sono alcuni meccanismi che lo permettono

Il livello di collegamento è implentato in tutte le interfacce di rete (in tutti gli host).

>[!note] Adattatori

Abbiamo due sottolivelli:
 - **Data Link Control (DLC)**: si occupa di tutte le funzioni *comuni* a tecnologie di trasmissione diverse (indipendenti dalla tecnologia).
 - **Media Access Control (MAC)**: si occupa solo degli aspetti specifici dei canali broadcast, cerca di ridurre il numero di collisioni ma non le elimina completamente

### Errori su singoli bit o a burst
Gli errori sono dovuti a interferenze di segnale che possono cambiare la forma del segnale.
Molto difficile avere un errore su singolo bit ma più probabile averlo a burst ovvero con più bit consecutivi.
Dipende dal *rumore* (durata dell'interferenza).

### Tecniche di rilevazione degli errori
EDC = Error detection and correction 
D = dati che devono essere protetti da errori ai queli vengono aggiunti bit EDC

>[!note] Controllo di parità
>Si va a vedere il numero di bit suddivisi ad 1 e si aggiunge uno 0 o 1 per avere un numero pari di bit impostati ad 1.
>Ci sono casi in cui non è efficente quindi conviene usare una *parità bidimensionale* (sia su righe che colonne)

## Protocolli di accesso multiplo
- **collegamento punto-punto**: viene usato il protocollo PPP (point to point protocol) del DLC.
- **collegamento broadcast**: dobbiamo gestire le collisioni, utilizziamo quindi il protocollo MAC per la gestione del canale condiviso. 

Ci sono tre categorie di protocolli di questo tipo:
1) *Protocolli a suddivisione di canale*
	1) ALOHA
	2) CSMA/CD
	3) CSMA/CA
2) *Protocolli ad accesso casuale*
	1) Reservation
	2) Polling
	3) Token passing
3) *Protocolli a rotazione*
	1) FDMA
	2) TDMA
	3) CDMA

## Protocolli ad accesso casuale
Nessuna stazione ha il controllo sulle altre.

>[!note] ALOHA
>Primo metodo casuale che è stato proposto in letteratura.
>**ALOHA puro**
>Ogni stazione può inviare un frame tutte le volte che ha dati da inviare. Il ricevente invia un ack e in base a questo il mittente agisce. 
>Se due stazioni ritrasmettono contemporaneamente si crea una collisione, quindi si attende un tempo random (*back off*) prima di effettuare nuovamente la trasmissione. La casualità aiuta ad evitare altre collisioni.
 >>[!warning] Studio dell'efficienza
 >
>**Slotted ALOHA**
>Divide il tempo in intervalli discreti (in slot) e i nodi devono essere sincronizzati affinché ognuno trasmetta un segnale solo all'interno del proprio slot.

>[!note] Accesso multiplo a rilevazione della portante (CSMA)
>Ci si pone in ascolto prima di trasmettere, se si rileva che il canale è libero si trasmette, altrimenti se è occupato si aspetta un intervallo di tempo.
>**CSMA/CD (rilevazione di collisione)**
>- Rileva la collisione in poco tempo
>- Annulla la trasmissione non appena si accorge che c'è un'altra tasmissione in corso.
>Mentre si inviano dati si ascolta il canale per capire se c'è una collisione. Questo è facile nelle LAN cablate ma difficile elle LAN wireless (non viene implementata).

**Dimensione minima del frame**: Una stazione un a volta inviato un frame non tiene una copia del frame né controlla il mezzo trasmissivo per rilevare collisioni, quindi deve controllare nel mentre della trasmissione, ovvero prima di inviare l'ultimo bit del frame.
**Metodi di persistenza**
Se un nodo trova un canale libero:
- Trasmette subito
	- Non- persistente
	- 1-Persistente
- Trasmette con probabilità p
	- p-persistente
Se un nodo trova un canale occupato
- Desiste
- Persiste rimanendo in ascolto finché non viene liberato

>[!note] Non persistente
>Se il canale è libero tra





 
 

