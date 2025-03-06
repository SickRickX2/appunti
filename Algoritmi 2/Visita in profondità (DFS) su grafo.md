>[!danger] Dato un grafo G ed un suo nodo *u* vogliamo sapere quali nodi del grafo sono raggiungibili a partire dal nodo *u*

![[Pasted image 20250306120940.png]]
## Rappresentato tramite matrice di adiacenza

```Python
def DFS(u,M):
	def DFSr(u,M,visitati):
		visitati[u] = 1
		for i in range(len(M)):
			

```