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

>[!note] Soluzione in $O(n)$
>```Python
>def BFS(x, G):
>	visitati = [0] * len(G)
>	visitati[x] = 1
>	coda = [x]
>	i = 0
>	while len(coda) > i:
>		u = coda[i]
>		i += 1
>		for y in G[u]:
>			if visitati[y] == 0:
>				visitati[y] = 1
>				coda.append(y)
>		return visitati
>		
>```

Esiste poi un'altra soluzione alternativa sempre con complessità $O(n+m)$ che fa uso della struttura dati **deque**.
Dal modulo python "collections" posso importare la struttura dati deque (double ended queue) che consente di effettuare inserimenti e cancellazioni da entrambi i lati di una lista in tempo $O(1)$ in particolare posso estrarre e inserire elementi a sinistra $popleft(), appendleft()$
```Python
def BFS(x, G):
	visitati = [0] * len(G)
	visitati[x] = 1
	from collections import deque
	coda = deque([X])
	while coda:
		u = coda.popleft()
		for y in G[u]:
			if visitati[y] == 0:
				visitati[y] = 1
				coda.append(y)
	return visitati
```
## BFS Vettore dei padri 

Modifichiamo la procedura in modo che restituisca in $O(n+m)$ l'albero di visita BFS rappresentato tramite il vettore dei padri.
![[Pasted image 20250317105715.png]]
```Python
def BFSpadri(x, G):
	P = [-1] * len(G)
	P[x] = x
	coda = [x]
	i = 0
	while len(coda) > 1:
		u = coda[i]
		i += 1
		for y in G[u]:
			if P[y] == -1
				P[y] = u
				coda.append(y)
	return P
```
vettore delle distanze

