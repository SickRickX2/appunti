Significa *stato del collegamento* ad ogni collegamento viene associato un valore che indica il suo costo. Se il costo è $\infty$ significa che il collegamento non è raggiungibile.

>[!note] Link State database
Il link-state database è dato dai costi sui link esistenti ed è unico per tutta la rete, ogni nodo contiene una copia. Viene rappresentato come una matrice.

Per costruire il database si utilizza il **flooding**
- ogni nodo deve conoscere i vicini con i relativi costi (viene fatto tramite messaggi di hello); viene creata la *link state packet* (viene inviato ai propri vicini e dovrà raggiungere tutti i nodi della rete).

Sul LSDB viene utilizzato l'algoritmo di Djikstra per creare una tabella di inoltro per ogni nodo.

Per costruire la tabella di routing ogni nodo applica l'algoritmo mettendo come radice sé stesso.

