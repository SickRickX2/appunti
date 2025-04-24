## Forwarding datagrammi IP
Inoltrare significa collocare il datagramma sul giusto percorso che lo porterà a destinazione, inviandolo al prossimo hop. L'inoltro richiede una riga nella tabella per ogni blocco di rete.

## Routing
Il routing costruisce e determina il percorso migliore da seguire che poi verrà usato dal forwarding (sempre tramite tabella).

## Routing intra-dominio: RIP
(*intradominio* vuol dire ad esempio all'interno di un ISP, viene fatto routing solo su una parte di rete e non su quella globale) 

>[!tip] Algoritmo Distance Vector
>- *Distribuito*: ogni nodo riceve informazione dai vicini e opera su quelle
>- *Asincrono* non richiede che tutti i nodi operino al passo con gli altri
>
>Si basa su:
>1) Equazione di Bellman-Ford
>2) Concetto di vettore di distanza
>
>**Equazione di Bellman-Ford**:
>Definisce
>$D_x(y):=$ il costo (o la distanza) del percorso a costo minimo dal nodo x al nodo y
>
>Allora:
>$D_x(y) = min_v\{c(x,v)+D_v(y)\}$
>dove $min_v$ riguarda tutti i vicini di x
>
>**Vettore distanza**
>Un albero a costo minimo è una combinazione di percorsi a costo minimo dalla radice dell'albero verso tutte le destinazioni.
>Il vettore di distanza è un array monodimensionale che rappresenta l'albero. Un vettore di distanza non fornisce il percorso da seguire per giunger alla destinazione ma solo i costi minimi per le destinazioni.
>>[!warning] Come viene creato il vettore distanza?
>>Ogni nodo della rete quando viene inizializzato crea un vettore distanza iniziale con le ingormazioni che il nodo riesce ad ottenere dai propri vicini (quelli a cui è collegato direttamente). Per creare il vettore dei vicini invia messaggi di *hello* attraverso le sue interfacce (e lo stesso fanno i vicini) e scopre l'identità dei vicini e la sua distanza da ognuno di essi. Il vettore iniziale rappresenta il vettore a costo minimo verso i vicini. Dopo che ogni nodo ha creato il suo vettore ne invia una copia ai suoi vicini.

 



