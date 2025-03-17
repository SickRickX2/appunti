>[!note] Distanza minima
>Dati due nodi $a$ e $b$ di un grafo $G$, definiamo *distanza minima* il numero minimo di archi che bisogna attraversare per raggiungere $b$ a partire da $a$. La distanza è posta a $+ \infty$ se $b$ non è raggiungibile partendo da $a$.
>![[Pasted image 20250317095608.png]]

>[!danger] Problema
>Dato un grafo $G$ ed un suo nodo x vogliamo conoscere le distanze di tutti i nodi di $G$ da $x$.

La *visita in ampiezza (Breadth First Search)* esplora i nodi del grafo da quelli a distanza 1 dalla sorgente $s$. Poi visita quelli a distanza 2 e così via. L'algoritmo visita tutti i vertici a livello $k$ prima di passare a quelli a livello $k+1$.
![[Pasted image 20250317100734.png]]


Durante la visita si genera un albero detto *albero BFS*, si visitano nodi sempre più distanti dalla radice.

Per effettuare questo tipo di visita manteniamo in una *coda* i nodi visitati i cui adiacenti non sono stati ancora esaminati. 
Ad ogni passo preleviamo il primo nodo dalla coda, esaminiamo i suoi adiacenti e se scopriamo un nuovo nodo lo visitiamo e lo aggiungiamo alla coda.
>[!tip] Soluzione sbagliata
>```Python
>def BFS(x, G):
>	visitati = [0] * len(G)
>	visitati[x] = 1
>	coda = [x]
>	while coda:
>		u = coda.pop(0)
>		for y in G[u]:
>			if visitati[y] == 0:
>				visitati[y] = 1 
>				coda.append(y)
>	return visitati
>```

Il codice di per sè funziona ma il problema risiede nella complessità
>[!warning] Complessità
>- Un nodo finisce in coda al più una volta. quindi il while verrà eseguito $O(n)$ volte.
>- Le liste di adiacnza dei nodi verranno scorse al più una volta quindi il costo totale dei $for y in G[u]$ sarà $O(m)$
>
>Se le operazioni di inserimento e cancellazione dalla coda richiedessero tempo $\Theta(1)$ avremmo complessità $O(n+m)$
>Il problema risiede proprio nell'implementazione della coda. Implementandola come una semplice lista il $pop(0)$ ha un costo di proporzionale al numero di elmenti in quel momento nella coda/lista e questi elementi possono essere anche $O(n)$.
>
>>[!danger] Quindi il costo di questa implementazione è $O(n^2)$

