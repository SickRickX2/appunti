La rete di accesso è composta da tutti quei dispositivi che permettono di collegarci al primo **edge router** collegato al backbone. 
## Struttura di Internet
La struttura di Internet è fondamentalmente gerarchica e ogni livello si basa su quello precedente.
>[!note] ISP di livello 1
Copertura nazionale/internazionale, collegati tramite cavi, anche sottomarini per attraversare l'oceano. Gli ISP sono direttamente  collegati tra di loro come pari.

>[!tip]  ISP di livello 2
Sono ISP più piccoli e utilizzano la rete del livello 1, sono quindi i loro clienti.

>[!example] ISP livello 3
>Sono ISP locali e sono le più vicine ai sistemi terminali.  Vengono chiamati anche ISP di accesso

Un pacchetto passa attraverso molte reti utilizzando quindi diversi ISP. Uno dei problemi principali delle reti è trovare la strada dei pacchetti per arrivare a destinazione, viene chiamato **routing** (instradamento).

La velocità della rete o di un collegamento significa quanto la rete trasmette e riceve velocemente i dati.
Per quanto riguarda il commutamento per le prestazioni ci sono diversi parametri che si misurano in termini di:
- ampiezza di banda
- bit rate
- throughput
- ritardi
- perdita di pacchetti
## Ampiezza di Banda
L'ampiezza di banda è una caratteristica del mezzo trasmissivo e ci dice quanto è in grado di trasmettere, rappresenta l'ampiezza del segnale di frequenze (più è ampio l'intervallo maggiori sono le informazioni veicolate attraverso il mezzo).

C'è anche una caratterizzazione di un collegamento, ovvero quanti bit si riesce a trasmettere al secondo. Il *rate* è la quantità di bit che un link riesce a trasmettere sul canale.

Quindi con il termine ampiezza di banda si indicano due concetti leggermente diversi ma strettamente legati.

1) **Caratterizzazione del canale o del sistema trasmissivo**: quantità che si misura in hertz e rappresenta la larghezza dell'intervallo di frequenze utilizzato dal sistema trasmissivo, ovvero l'intervallo di frequenze che un mezzo fisico conscente di trasmettere senza danneggiare il segnale in maniera irrecuperabile. Maggiore è l'ampiezza di banda, maggiore è l'informazione che può essere veicolata attraverso il mezzo trasmissivo
2) **Caratterizzazione di un collegamento**: quantità espressa in bit al secondo (bps), detta anche *bit transmission rate (velocità di trasmissione)*
>[!note] Bit rate
>Dipende dalla banda e dalla specifica tecnica di trasmissione, è proporzionale alla banda in hertz. Per **banda** di un tipo di rete si intende il **bit rate garantito nominalmente** dai suoi link, il rate fornisce un'indicazione della capacità della rete di trasferire dati.

## Throughput
Indica quanto velocemente riusciamo ***effettivamente*** a inviare dati tramite una rete. Quindi è il numero di bit al secondo che passano attraverso un punto della rete.
Somiglia al rate ma:
- è solitamente minore o uguale al rate, perché il rate è una misura potenziale mentre il throughput è una misura effettiva e può variare in ogni momento

Un pacchetto durante il viaggio a destinazione può attraversare numerosi link ognuno con un throughput diverso, per calcolare il throughput medio basta calcolare il throughput minimo tra tutti i link.
>[!warning] Collo di bottiglia
>Collegamento su un percorso punto a punto che vincola un throughput end to end

Nel caso in cui abbiamo più terminali, il throughput viene suddiviso in base al numero di terminali.
>[!example] Esempio
>Il rate 

## Latenze
Latenza ( ritardo o delay): quanto tempo serve affinché un pacchetto arrivi completamente a destinazione dal momento in cui il primo bit parte dalla sorgente. Ci sono diversi fattori che determinano la latenza di un pacchetto perché passa attraverso diversi link e router.
1) Ritardo di elaborazione del nodo (processing delay): il paccehtto arriva e si controlla l'integrità, (in caso negativo viene scartato) poi viene determinato il canale d'uscita e infine c'è il tempo dalla ricezione del pacchetto alla consegna alla porta output
2) Ritardo di accodamento (queuing delay): il pacchetto viene messo in coda sul buffer d'uscita o d'entrata, questo dipende dal livello di congestione del router(numero di pacchetti nelle code del router). Questo ritardo può variare da pacchetto a pacchetto.
3) Ritardo di trasmissione: dipende dal canale ed è il tempo richiesto per inserire tutto il pacchetto sul collegamento (trasmissione) L/R ( quanti pacchetti devo spedire fratto il rate)
4) Ritardo di propagazione:  quanto tempo impiega un pacchetto per propagarsi sul canale una volta immesso, ovvero il viaggio sul canale (s = velocità di propagazione per il simbolo bit che corrisponde alla velocità della luce, d = lunghezza del collegamento fisisco Ritardo di propagazione = d/s)
Il ritardo di trasmissione è solo il tempo per uscire mentre la propagazione è il viaggio.

Per calcoalre il ritardo di un pacchetto, vanno considerati tutti e 4 i ritardi.

Il ritardo di accodamento dipende da pacchettoa pacchetto, dal tasso di arrivo, dal rate e dalla lunghezza dei pacchetti.
R = rate
L = lunghezza
a = tasso medio di arrivo dei pacchetti
intensità di traffico =  La / R

se:
- La/R = 0 poco ritardo
- La/R => 1 il ritardo si fa consistente
- La/R > 1 sto cheidendo più lavoro di quello che può essere svolto

## Perdita di pacchetti
Se ho un'intensità elevata le code si riempiono e i pacchetti che arrivano vengono persi perchè il router non è in grado di memorizzarli. Se il pezzo di dati viene perso il pacchetto dovrà essee ritrasmesso e in questo modo aumenta il ritardo.


C'è un comando *traceroute* che permette di fare una stima del ritardo.
L'outpur presenta 6 colonne:
7) numero di router sulla rotta
8) nome del router
9) indirizzo del router
10) tempo di andata eritorno del 1 pacchetto
11) // del secondo
12) // del terzo
Il tempo di andata e ritorno *round trip time* include i 4 ritardi. Se un pacchetto non riceve rsiposta da un router intermedio o ne riceve meno di 3 allora pone un asterisco al posto del tempo RTT.

>[!note] Prodotto Rate * Ritardo
>Il prodotto ci dice il numero di bit che possono riempire il collegamento.

>[!danger] Esercizio per casa
>Pacchetto = 1000 byte
>collegamento = 2500km
>velocità = 2,5 x 10^8 m/s
>rate = 2 Mbps



2500 : 2 = 1250 (ritardo di )


