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

## Rappresentato tramite lista di adiacenza
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
DFS(u,M,visitati)
return [x for x in range(n) if visitati[x]]

```