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

#### No collision detection
Nel wireless non possiamo usare il protocollo CSMA/CD; per rilevare una collisione un host deve poter trasmettere e ricevere contemporaneamente. Poiché la potenza del segnale ricevuto è molto inferiore a quella del segnale tramsessio, sarebbe troppo costoso usare un adattatore di rete in grado di rilevare le collisioni.
#### Hidden terminal problem
Un host potrebbe non accorgersi che un altro host sta trasmettendo e quindi non sarebbe in grado di rilevare la collisione (ascoltando il canale).

## IEEE 802.11
IEEE ha definito le specifiche per le LAN wireless, chiamate 802.11, che coprono i livelli fisico e di collegamento.
**Architettura: BSS**: *basic service set* è costiuita da uno o più host wireless e da un accesso point
**Architettura: ESS** *extended service set* è costituito da due o più BSS con infrastruttura. I BSS sono collegati tramite un sistema di distribuzione che è una rete cablata o wireless. Quando i BSS sono collegati, le stazini in visibilità comunicano direttamente mentre le altre comunicano tramite l'AP.

## Canali e Associazione
Lo spettro 2.4 GHz - 2.485 GHz è diviso in 11 canali parzialmente sovrapposti. L'amministratore dell'AP sceglie una frequenza, sono possibili interferenze. Il numero massimo di frequenza utilizzabili da diversi AP per evitare interferenze è 3(usando i canali *1,6,11*). I canali non interferiscono se separati da 4 co più canali.
L'architettura IEEE 802.11 prevede che una stazione wireless si associ a un AP per accedere a Internet.

**Associazione di una stazione a un AP:** è necessario conoscere gli AP disponibili in un BSS ed è necessario un protocollo di associazione:
- AP invia segnali periodici (*beacon*) che includono l'identificatore dell'AP (*Service Set Identifier- SSID*) e il suo indirizzo MAC
- La stazione wireless che vuole entrare in un BSS scandisce gli 11 canali trasmissivi alla ricerca di frame beacon (*passive scanning*)
- Alla fine della scansione la stazione sceglie l'AP da cui ha ricevuto il beacon con la maggiore potenza di segnale e gli invia un frame con la richiesta di associazione
- L'AP accetta la richiesta con un frame di risposta associazione che permetterà all'host entrante di inviare una richiesta DHCP per ottenere un indirizzo IP
- Può essere prevista un'autenticazione per eseguire l'associazione

>[!tip] Protocollo MAC 802.11
>Più stazioni possono voler comunicare nello stesso momento.
>Abbiamo quindi due tecniche di accesso al mezzo:
>1) *Distributed Coordination Function (DCF)*: in cui i nodi si contendono l'accesso al canale
>2) *Point coordination function (PCF)*: in cui non c'è contesa e l'AP coordina l'accesso dei nodi al canale

### CSMA/CA
*CSMA/Collision Avoidance*
Evitare le collisioni: due o più nodi trasmettono contemporaneamente
Carrier sense: ascoltare il canale prima di trasmettere
No collision detection per 3 motivi:
1) Impossibilità di trasmettere e ricevere contemporaneamente 
2) Hidden terminal problem
3) Raggio di trasmissione limitato (difficile sentire tutte le trasmissioni)
>[!danger] ACK
>Con gli ack ci sarebbe bisogno di un doppio carrier sense (dati e ack) e ci sarebbe comunque ci sarebbe la possibilità di collisione anche su ack.

>[!note] IFS (spazio interframe)
>Rilevata la portante, se il canale risulta libero, si posticipa la trasmissione per evitare che stazioni che hanno già iniziato a trasmettere collidano con la stazione che vuole trasmettere.
>- SIFS: Short IFS realizza alta priorità
>- DIFS: Distributed IFS realizza bassa priorità
>
>![[Pasted image 20250519112034.png|200]]
>**Mittente:** ascolta il canale
>	Se libero per DIFS tempo allora trasmette
>**Ricevente**: 
>	Se frame ricevuto correttamente invia ACK dopo SIFS tempo
>
>Se durante l'intervallo DIFS il canale diventa occupato:
>- l nodo *interrompe il conteggio* del DIFS.
>- *Aspetta* che il canale torni *completamente libero*
>- Quando il canle torna libero, *riavvia da zero* il conteggio del DIFS completo

>[!tip] Finestra di contesa
>Dopo aver atteso un tempo IFS, se il canle è ancora inattivo, la stazione attende un ulteriore tempo di contesa.
>**Finestra di contesa**(Contention window): lasso di tempo (backoff) per cui deve sentire il canale libero prima di trasmettere
>	- Sceglie R random in \[0,CW]
>	- While R>0:
>		- ascolta il canale per uno slot
>		- Se il canle è libero per la durata dello slot -> R:=R-1
>		- altrimenti attende (interrompe il timer e aspetta che il canale si liberi e riavvia il timer)

#### DIFS + Finestra di Contesa
**Fase 1: Attesa dell'IFS**
- Il nodo rileva il canale *libero*
- Attendde un tempo fisso: *DIFS*
- Se il canale *rimane libero* per tutto il DIFS -> passa alla *finestra di contesa*
**Fase 2: Finestra di contesa (Backoff)**
- Il nodo *sceglie un numero casuale* in un intervallo \[0, CW-1], dove *CW* è la *Contention Window*
- Ogni unità di tempo della finestra si chiama *Slot Time*
- Il nodo *inizia a contare all'indietro* (backoff counter), *solo se il canale rimane libero*
#### CSMA/CA: RTS/CTS
Il problema dell'hidden terminal non viene risolto con IFS e finestra di contesa, è necessario un meccanismo di prenotazione del canale: *Request-to-send(RTS)*,*Clear-to-send(CTS)*

>[!note] ACK
>È necessario utilizzare riscontri positivi e timer per capire se la trasmissione è andata a buon fine.
>- Il mittente *non può aspettare l'ACK all'infinito*
>- Imposta quindi un ACK timeout
>- Se il timer *scade senza aver ricevuto l'ACK* il nodo *suppone che la trasmissione sia fallita* e tenta una ritrasmissione

## Network Allocation Vector (NAV)
Quando una stazione invia un frame RTS include la durata di tempo in  cui occuperà il canale per trasmettere il frame e ricevere l'ack. Questo tempo viene incluso anche nel CTS. Le stazioni che sono influenzate da tale trasmissione avviano un timer chiamato NAV che indica quanto tempo devono attendere prima di eseguire il sensing del canale. Ogni stazione prima di ascoltare verifica il NAV.

>[!warning] Collisioni durante l'handshaking
>Cosa succede se avviene una collisione durante la trasmissione di **RTS o CTS**?
>Se il mittente non riceve CTS allora assume che c'è stata collisione e riprova dopo un tempo di backoff.

>[!note] Formato del frame
>![[Pasted image 20250520114017.png]]
>*Frame control (FC):* tipo di frame e alcune informazioni di controllo
>*D:* durata della trasmissione, usata per impostare il NAV (Impostata sia per DATA che per RTS, CTS frame)
>*Indirizzi*: indirizzi MAC (descritti in seguito)
>*SC:* informazioni sui frammenti ( #frammento e #sequenza). Il numero di sequenza serve per distinguere frame ritrasmessi come nel livello trasporto (ACK possono andare perduti)
>*Frame Body:* playload
>*FCS:* codice CRC a 32 bit
> 

#### Mobilità 
All'interno della stessa sottorete IP, semplice all'interno della stessa rete; l'indirizzo IP rimane lo stesso.
>[!warning] Come avviene il cambio di AP mantenendo attive tutte le connessioni TCP?

![[Pasted image 20250520114448.png|375]]
- H1 sente che il segnale da AP1 si affievolisce e avvia una scansione per un segnale più forte 
- H1 rileva AP2, si disassocia da AP1 e si associa a AP2, mantenendo lo stesso IP e sessioni TCP
Come si comporta lo switch?
- Autoimpara ma non può supportare utenti con elevata mobilità
- AP2 invia un frame broadcast allo switch con indirizzo mittente H1 e lo switch capisce che H1 è ora nel BSS2
- Un protocollo inter-AP è in via di sviluppo






