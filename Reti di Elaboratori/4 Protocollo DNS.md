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

