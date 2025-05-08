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
D