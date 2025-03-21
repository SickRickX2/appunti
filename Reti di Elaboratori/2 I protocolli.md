## Protocollo
Un protocollo definisce le regole che il mittente e destinatario devono rispettare per una corretta comunicazione.

>[!note] Principi della strutturazione a livelli
>**Strutturazione a livelli**: questa strutturazione consente di suddividere un compito complesso in compiti più semplici:
>- *Modularizzazione* (indipendenza dei livelli)
>- *Collegamento logico*: i livelli logicamente sono direttamente collegati, ovvero il protocollo implementato permette la comunicazione tra i livelli che si trovano pari (peer) tra di loro.

>[!note] Stack protocollare TCP/IP
>Sono i due protocolli principali di tutto lo stack, si tratta di una gerarchia di protocolli costituita da moduli interagenti tra loro.

**Applicazione** è la sede delle applicazioni di rete:
- HTTP (protocollo che regalo la comunicazione col web) ([[3 HTTP]]), SMTP, (mail) FTP(file), DNS (generale) ([[4 Protocollo DNS]])
- I pacchetti sono denominati *messaggi*
**Trasporto** trasferimento dei messaggi a livello di applicazione tra il modulo client e server di un'applicazione
- TCP (affidabile), UDP (non affidabile)
- I pacchetti sono denominati *segmenti* (per tcp) e *datagramma utente per* (udp)

**Rete** implementa l'instradamento dei segmenti dalla sorgente alla destinazione e deve far in modo che i pacchetti seguano il percorso scelto
- IP, protocolli di instradamento
- I pacchetti sono denominati *datagrammi*

**Link (collegamento)** si occupa di trasmettere i datagrammi da un nodo a quello successivo sul percorso 
- Ethernet, WI-Fi, PPP
- I pacchetti sono denominati *frame*

**Fisico** il trasferimento fisico dei *bit* lungo il canale di comunicazione

 I router e gli switch non implementano l'intero stack protocollare ma solo una parte, questo perché non ci sono utenti che devono usare le applicazioni ma devono fare cose diverse.
## Servizi e protocolli
Un servizio è un **insieme di primitive** che uno **strato offre a quello superiore**. Mentre un protocollo è l'insieme di regole che controllano il formato e la comunicazione tra pari.

>[!note] Incapsulamento e decapsulamento
>Quando il pacchetto **"scende"** ad ogni livello viene incapsulato, vengono **aggiunte** mano mano **informazioni per gestire** quel pacchetto. Queste informazioni vengono denominate *"intestazioni"* e ogni livello ha la propria.
>Invece **"salendo" verrà decapsulato**, verranno man mano tolte le intestazioni di ogni livello.

>[!note] Multiplexing e demultiplexing
>Dato che lo stack protocollare prevede più protocolli nello stesso livello è necessario eseguire mutliplexing alla sorgente e demultiplexing a destinazione. A ogni livello viene aggiunto un'identificativo su chi ha "passato" il pacchetto (*numero di porta*)

## Modello OSI
L'ISO organizzazione dedicata alla definizione di standard universali ha definito il modello OSI come modello alternativo al TCP/IP. Non ha mai preso piede per diversi motivi
1) Il tcp/ip già era diffuso
2) Alcuni livelli non sono mai stati specificati completamente

## Standard
Uno standard è una specifica di regole prima studiata e in seguito universalmente accettata.

## Modello TCP/IP: Applicazione
## L'offerta di servizi
- Protocolli Standard
	Esistono diversi protocolli di livello applicazioni che sono standardizzati e documentaiti dagli enti responsabili della gestione di Internet
- Protocolli non standard
	Si possono creare applicazioni non standard scrivendo due programmi che forniscono servizi agli utenti. Non è necessario chiedere autorizzazioni.

>[!note] Creare un'applicazione di rete
>Scrivere programmi che girano su sistemi terminali diversi e comunicano attraverso la rete. I programmi applicativi sono indipendenti dalla tecnologia che c'è sotto
>Bisogna scegliere il tipo di architettura:
>- Client-server
>- Peer-to-peer
>Tipo di comunicazione e di servizi,ecc
>In base a queste scelte verrano usati diversi paradigmi.


