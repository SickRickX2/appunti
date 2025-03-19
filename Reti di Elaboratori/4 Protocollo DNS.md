## Identificazione degli host
Gli **host internet** hanno *nomi* (hostname)
	es: www.google.com
I nomi sono facili da ricordare ma forniscono poca informazione sulla collocazione degli host all'interno di Internet.

Gli **indirizzi IP** per gli host sono formati da 32 bit e vengono usati per indirizzare i datagrammi (più appropriato per le macchine)
>[!note] Indirizzo IP
>Consiste di 4 byte, è costituito da una stringa in cui ogni punto separa uno dei byte espressi con un numero decimale compreso tra 0 e 255.
>Presenta una struttura **gerarchica**:
>- rete di apparatenenza
>- indirizzo nodo

>[!danger] Come recuperare un indirizzo IP da un nome?

# DNS: Domain Name System
![[Pasted image 20250316201344.png]]
>[!note] Servizio DNS
>- **Memorizzazione** -> *Database distribuito* implementato in una gerarchia di **server DNS**
>- **Accessibilità**-> *Protocollo a livello applicazione* che consente agli host di interrogare il database distribuito per risolvere i nomi  (tradurre indirizzi/nomi)
>
>Il DNS viene utilizzato dagli altri protocolli di livello applicazione (HTTP, SMTP, FTP) per tradurrre hostname in indirizzi IP, utilizza il trasporto UDP e indirizza la porta 53

>[!example] Esempio di interazione con HTTP
>Un browser (ossia client HTTP) di un host utente richiede la URL www.someschool.edu
>1) L'host esegue il lato client dell'applicazione
>2) Il browser estrae il nome dell'host www.someschool.edu dall'URL e lo passa al lato client dell'applicazione DNS
>3) Il client DNS invia una query contenente l'hostname a un server DNS
>4) Il client DNS riceve una ripsopsta che include l'indirizzo IP corrispondente all'hostname
>5) Ottenuto l'indirizzo IP dal DNS, il browser può dare inizio alla connessione TCP verso il server HTTP localizzato a quell'indirizzo IP

**DNS è un'applicazione?**
DNS è un protocollo del livello applicazione, viene eseguito dagli end systems secondo il paradigma client server.  Utilizza un protocollo di trasporto end-to-end per trasferire messaggi tra gli end system (UDP).

Non è un'applicazione con cui gli utenti interagiscono direttamente (eccetto amministratori di rete).

Fornisce una funzionalità di base di internet per le applicazioni utente. Rispecchia la filosofia di concentrare la complessità nelle parti periferiche della rete.
## Servizi DNS
>[!note] Aliasing
>Permette di associare un nome più semplice da ricordare a un nome complesso.
>**Host aliasing**: un host può avere uno o più sinonimi (alias). Il DNS può essere invocato da un'applicazione per l'hostname canonico così come l'IP.
>
>**Mail server aliasing**: spesso i mail server e il web server di una società hanno lo stesso alias, ma nomi canonici diversi.

>[!note] Distribuzione del carico 
>DNS viene utilizzato per distribuire il carico tra server replicati.
>Il DNS contiene l'insieme di indirizzi IP. Quando un client effettua una richiesta DNS per un nome mappato in un insieme di indirizzi, il server risponde con l'insime di indirizzi ma variando l'ordinamento a ogni risposta.

Il DNS non può essere centralizzato, ovvero memorizzare il database su un singolo server. Perché se crasha quel singolo server crasha Internet. In secondo luogo non potrebbe gestire tutto il traffico che sarebbe elevato.

Il mapping è quindi distribuito su svariati server DNS.

## Gerarchia server DNS
Ci sono 3 classi di server DNS organizzati in una gerarchia
- **Root**
- **Top-level domain (TLD)**
- **Authoritative**
Ci sono poi i server DNS locali con cui interagiscono direttamente le applicazioni.
![[Pasted image 20250319160535.png]]
>[!note] DNS: Root
>In Internet ci sono 13 server DNS radice. Ognuno di questi server è replicato per motivi di sicurezza e affidibilità. I root server vengono contattati dai server DNS locali.
>Server DNS radice: 
>- contatta un server DNS TLD se non conosce la mappatura
>- ottiene la mappatura
>- restituisce la mappatura al server DNS locale

>[!note] DNS: TLD e server di competenza
>*Server TLD (top level domain)*: si occupano dei domini com, org, net, edu... e di tutti i domini locali di alto livello quali it, uk, fr, ca e jp. La compagnia Verisign Global Registry Services gestice i server TLD per il dominio **com**.
>Il Registro.it che ha sede a Pisa all'instituto di Informaitca e Telematica (CNR) gestisce il dominio it.
>
>*Server di competenza (authoritative server)*: ogni organizzazione dotata di host Internet pubblicamente accessibili (quali i server web e i server di posta) deve fornire i record DNS di pubblico dominio che mappano i nomi di tali host in indirizzi IP. Possono essere mantenuti dall'organizzazione (università) o da un service provider.
>In genere sono due server (primario e secondario).

>[!note] DNS: locale
>Non appartiene strettamente alla gerarchia dei server. Ciascun ISP (università, società, ISP residenziale) ha un server DNS locale.
>Quando un host effettua una richiesta DNS, la query viene inviata al suo server DNS locale.
>Quando un host effettua una richiesta DNS, la query viene inviata al suo server DNS locale. Il server DNS locale opera da proxy e inoltra la query in una gerarchia di server DNS

>[!tip] Caching
>DNS sfrutta il caching per migliorare le prestazioni di ritardo e per ridurre il numero di messaggi DNS che "rimbalzano" in Internet. Una volta che il server DNS impara la mappatura, la mette nella **cache**.

## Record e messaggi
