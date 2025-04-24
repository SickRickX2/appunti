>[!note] IPv4
>Ogni interfaccia di un host ha un indirizzo IP univoco a 32 bit.
>>[!warning] Dipende dalla rete
>>Non dipende dall'host, se mi connetto via wireless o via ethernet l'indirizzo IP cambia.
>
>Sono valori che vanno da 1 a 255.

>[!tip] Interfaccia
>L'interfaccia è il confine tra host e collegamento fisico. I rputer devono necessariamente essere connessi ad almeno due collegamenti. Un'host in geneere ha un'interfaccia e a ciascuna interfaccia è associato un indirizzo IP.

### Spazio degli indirizzi
Numero totale indirizzi $2^{32}$ ovvero più di 4 miliardi.
![[Pasted image 20250424100918.png]]
Abbiamo un prefisso che identifica la rete e un suffisso che individua l'host.
Il **prefisso** può avere lunghezza:
- *fissa*: indirizzamento con classi (multipli di 8)
- *variabile*: indirizzamento senza classi

>[!tip] Pro e contro di prefisso fisso
>- Problema dell'esaurimento degli indirizzi: un problema comune a tutti gli indirizzi iniziale tranne per il C che aveva un numero di reti maggiori ma non bastava lo spazio.

>[!note] Indirizzamento senza classi
>Nasce dalla necessità di maggiore flessibilità nell'assegnamento degli indirizzi. Vengono utilizzati blocchi di lunghezza variabile che non appartengono a nessuna classe, motivo per cui un indirizzo non è in grado di definire da solo la rete (o blocco) a cui appartiene. La lunghezza del prefisso è dunque variabile e viene distinta dal suffisso tramite un



Per questo vengono utilizzati blocchi di lunghezza variabile, ma non si può sapere come vengono suddivisi i blocchi. Si utilizza quindi /+numero per sapere quanti bit vengono allocati per quel blocco(*Notazione CIDR, Classless InterDomain Routing*)

>[!note] Estrazione delle informazioni
>Se n è lunghezza del prefisso:
>1) Il numero di indirizzi nel blocco è dato da N = 2^32-n
>2) Per trovare il primo indirizzo si impostano a 0 tutti i bit del prefisso
>3) Per trovare l'ultimo indirizzo si impostano a 1 tutti i bit del suffisso

### Maschera e indirizzo di rete
**Maschera dell'indirizzo**: numero composto da 32 bit in cui i primi n bit a sinistra sono impostati a 1 e il resto (32-n) a 0. Mediante la maschera si ottiene l'indirizzo di rete che è usato nell'instradamento dei datagrammi verso la destinazione.

## Indirizzi IP speciali
Indirizzi nella forma 127.xx.yy.zz sono riservati ai **loopback** (usato dai programmatori per simulare l'invio di un messaggio in rete ma in realtà è in locale)
## Distribuzione indirizzi all'interno di una rete LAN

Bisogna contattare il proprio ISP e ottenere un blocco di indirizzi contigui e con un prefisso comune. Un ISP a sua volta contatta **ICANN**.

>[!danger] Come ottenere un indirizzo IP
>Per assegnare un indirizzo IP ad un host si utilizza il protocollo DHCP, nel momento in cui ci si collega gestisce l'insieme di indirizzi IP disponibili sulla rete, assegnandoli a chi ne fa richiesta. Gli indirizzi vengono assegnati dinamicamente per un determinato lasso di tempo.

>[!note] DHCP Dynamic Host Configuration Protocol
>Assegna in maniera automatica degli indirizzi (programma di tipo client server) ai singoli host o router. Questo protcollo si basa su 4 messaggi:
>- DHCP discover
>- DHCP offer
>- DHCP request
>- DHCP ack
>
> Implementa una funziponalità di rete ma effettivamete è implementato a livello applicazione.

## Sottorete
Meccanismo che ci permette di usare degli *indirizzi priviati*.
Una **sottorete** è una rete collegata solo ad un interdaccia di un host o di un router.

Si è deciso di privatizzare alcuni blocchi di indirizzi per risolvere il problema della necessità di avere sempre più indirizzi IP.

Non sono disponibili nella rete ma sono disponibili solo alla connessione locale (lan).

>[!note] NAT Network Address Translation
>L'indirizzo privato viene convertito in un indirizzo pubblico (e viceversa da se il messaggio viene da fuori).
>Basta un solo indirizzo pubblico per gestire più indirizzi privati. Per identificare gli host privati sulla rete privata, si usa il numero di porta (solo come valore)

>[!tip] Forwarding datagrammi IP
>Inoltrare significa collocare il datagramma siul giusto percorso per arrivare a destinazione. Inviare il datagramma al prossimo hop. 
>Dall'host arriva al router locale, dopodiché accede alla tabella di routing per individuare il prossimo hop.

>[!note] ICMP
>Viene usato da host e router per scambiarsi informazioni a livello di rete. Utilizza IP per mandare i proprio datagrammi, hanno un campo **tipo** e un campo **codice** e contengono l'intestazione e i primi 8 byte del datagramma IP che ha provocato la generazione del messaggio.

>[!tip] Ping
>Applicazione utilizzata per inviare una richiesta echo sulle macchine

>[!tip] Traceroute
>Utilizza il protocollo ICMP.
