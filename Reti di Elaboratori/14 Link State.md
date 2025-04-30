Significa *stato del collegamento* ad ogni collegamento viene associato un valore che indica il suo costo. Se il costo è $\infty$ significa che il collegamento non è raggiungibile.

>[!note] Link State database LSDB
Il link-state database è dato dai costi sui link esistenti ed è unico per tutta la rete, ogni nodo contiene una copia. Viene rappresentato come una matrice.
>![[Pasted image 20250430180439.png|200]]

Per costruire il database si utilizza il **flooding**
- ogni nodo deve conoscere i vicini con i relativi costi (viene fatto tramite *messaggi di hello*); viene creata la *link state packet*, la lista dei vicini con i relativi costi dei collegamenti (viene inviato ai propri vicini e dovrà raggiungere tutti i nodi della rete).
- Ogni nodo invia messaggi di hello per conoscere i propri vicini e il loro costo creando così il LS packet
- **Flooding del LSP**: si invia su ogni interfaccia ad esclusione di quella da cui si è ricevuto il pacchetto

Sul **LSDB** viene utilizzato l'*algoritmo di Djikstra* per creare una tabella di inoltro per ogni nodo.

Per costruire la tabella di routing ogni nodo applica l'algoritmo mettendo come radice sé stesso.

## Algoritmo di instradamento a stato del collegamento
**Algoritmo di Dijkstra**
La topologi 

## Protocollo di Routing
OSPF Open Shortest PAth First (implementato da IP, quindi a livello di rete e non applicazione) utilizza il flooding inizialmente e in seguito l'algoritmo di Dijkstra. I messaggi OSPF vengono incapsulati in datagrammi IP 
 TIpologie:
 - Hello: usato dal router per conoscere i vicini e farsi conoscere
 - Database description: una risposta ad hello
 - Link State Request: per chiedere specifiche informazioni sul collegamento
 - Link state update: messaggio principale per la costruzione del database
 - Link State ACK: risposta all'update