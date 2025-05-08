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
 >>[!tip] Studio dell'efficienza
 >
>**Slotted ALOHA**
>Divide il tempo in intervalli discreti (in slot) e i nodi devono essere sincronizzati affinché ognuno trasmetta un segnale solo all'interno del proprio slot.




 
 

