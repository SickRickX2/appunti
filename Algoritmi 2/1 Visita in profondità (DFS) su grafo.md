>[!danger] Dato un grafo G ed un suo nodo *u* vogliamo sapere quali nodi del grafo sono raggiungibili a partire dal nodo *u*

![[Pasted image 20250306120940.png]]
## Rappresentato tramite matrice di adiacenza

```Python
def DFS(u,M):
	def DFSr(u,M,visitati):
		visitati[u] = 1
		for i in range(len(M)):
			if M[u][i] == 1 and not visitati[i]:
				DFSr(i,M,visitati)
###
n = len(M)
visitati = [0] * n
DFS(u,M,visitati)
return [x for x in range(n) if visitati[x]]
```
Al termine di *DFS(u, M)* si ha ```visitati[i]``` se e solo se *i* è raggiungibile da *u*
>[!tip] Costo dell'algoritmo
>La complessità della procedura è $O(n)\times\Theta(n) = O(n^2)$
>>[!warning]  Spiegazione
>>Il costo dell'algoritmo viene giustificato perché all'interno di DFSr:
>>- Il *primo for* lo eseguiamo *esattamente n volte* quindi $\Theta(n)$
>>- La *chiamata ricorsiva* a seguito dell'if statement, ovvero la visita, viene eseguita *al massimo n volte* se tutti i nodi sono raggiungibili partendo dal nodo u

## Rappresentato tramite liste di adiacenza
Questo algoritmo è più veloce proprio grazie al tipo di rappresentazione del grafo, ovvero tramite liste di adiacenza
```Python
def DFS(u,G):
	def DFSr(u,G,visitati):
		visitati[u] = 1
		for nodo in G[u]:
			if not visistati[v]:
				DFSr(nodo,G,visitati)
###
n = len(M)
visitati = [0] * n
DFS(u,G,visitati)
return [x for x in range(n) if visitati[x]]

```
Esattamente come prima, al termine di *DFS(u, M)*  si ha ```visitati[i]``` se e solo se *i* è raggiungibile da *u*. 
>[!tip] Costo dell'algoritmo
>La complessià della procedura è $O(n+m)$ --->$O(n)$
>>[!warning] Spiegazione
>>La complessità dell'algoritmo vien giustificata perché visitiamo gli elementi della lista di adiacenza del nodo che corrispond al numero di archi, e in seguito eseguiamo la visita sui nodi al più n volte se sono raggiungibili tutti i nodi del grafo

## Alberi DFS
Con una visita DFS gli archi si bipartiscono in quelli che nel corso della visita sono stati attraversati (perché permettevano di raggiungere nuovi nodi) e gli altri:
I *nodi visitati* e gli *archi effettivamente attraversati* formano un albero detto **albero DFS**.