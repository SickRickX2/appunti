## Forwarding datagrammi IP
Inoltrare significa collocare il datagramma sul giusto percorso che lo porterà a destinazione, inviandolo al prossimo hop. L'inoltro richiede una riga nella tabella per ogni blocco di rete.

## Routing
Il routing costruisce e determina il percorso migliore da seguire che poi verrà usato dal forwarding (sempre tramite tabella).

## Routing intra-dominio: RIP
(*intradominio* vuol dire ad esempio all'interno di un ISP, viene fatto routing solo su una parte di rete e non su quella globale) 

>[!tip] Algoritmo Distance Vector
>- *Distribuito*: ogni nodo riceve informazione dai vicini e opera su quelle
>- *Asincrono* non richiede che tutti i nodi operino al passo con gli altri
>Si basa su:
>1) Equazione di Bellman-Ford
>2) Concetto di vettore di distanza