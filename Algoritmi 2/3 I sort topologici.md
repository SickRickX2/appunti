L'ordinamento topologico consiste nell'ordinare tutti i nodi del grafo in maniera tale che gli archi vadano tutti da sinistra verso destra (o viceversa).
Questo tipo di ordinamento è utile perché i grafu diretti possono catturare relazioni di propedeuticità (un arco da *a* a *b* indica che *a*  è propedeutico a *b*)

Un grafo diretto può avere da 0 fino a n! ordinamenti topologici.
Un algoritmo esaustivo per il problema (che genera sistematicamente i differenti ordinamenti dei nodi del grafo e per ciascuno di questi testa se il vincolo sugli archi risulta soddisfatto) ha complessità $\Omega(n!)$ ed è quindi improponibile.

>![!note] DAG
>Affinché un grafo G possa avere un ordinamento topologico è necessario che sia un DAG (Grafo Diretto Aciclico).
>