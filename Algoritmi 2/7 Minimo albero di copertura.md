*Problema:* dato un grafo G connesso e pesato, cerchiamo un suo minimo albero di copertura.

>[!note] Algoritmo di Kruskal
>- Parti con il grafo T che contiene tutti i nodi di G e nessun arco di G
>- Considera uno dopo l'altro gli archi del grafo G in ordine di costo crescente
>- Se l'arco forma un ciclo in T con archi già presi allora non prenderlo, altrimenti inseriscilo in T
>- Al termine restituisci T
>
>(L'algoritmo rientra nel *paradigma della tecnica greedy*)
>- La sequenza di *decisioni è irrevocabile*
>- Le decisioni vengono prese in base ad un *criterio "locale"*

>[!example] Esecuzione
>Grafo di partenza:
>![[Pasted image 20250321112622.png|350]]
>![[Pasted image 20250321112645.png|400]]
>![[Pasted image 20250321112657.png|400]]

>[!tip] Pseudocodice
>```
>kruskal(G):
>	T = set()
>	inizializza E con gli archi di G
>	while E ≠ []:
>		estrai da E un arco(x, y) di peso minimo
>		if l'inserimento di (x, y) in T non crea ciclo con gli archi in T:
>			inserisci arco(x, y) in T
>		return T
>
>```

*Correttezza*
Dobbiamo dimostrare che al termine dell'algoritmo T è un albero di copertura e che non c'è un altro albero che costa meno.

- *Produce un albero di copertura*. La prova è per assurdo. Supponiamo che al termine in T ci sia più di una componenete. Consideriamo A, poiché G è connesso nel grafo c'è un arco (x,y) da un nodo x di A ad un nodo y di un'altra componente B ma l'arco (x, y) ad un certo punto è stato estratto da E e se non crea ciclo in T ora che l'algoritmo non lo creava neanche al momento in cui è stato estratto e quindi sarebbe stato aggiunto a T e non scartato.
- *Non c'è un albero di copertura per G che costa meno di T.* La prova è per assurdo. Tra tutti gil alberi di copertura di costo minimo per G prendiamo quello che differisce nel minor numero di archi da T. Sia T*. Supponiamo per assurdo che T differisca da T*. Dimostreremo che questa assunzione porterebbe all'assurdo perché avrebbe come conseguenza l'esistenza di un altro albero di copertura di costo minimo per G che differisce da T in meno archi di T*. Consideriamo l'ordine $e_1, e_2, e_3, ...$ con cui gli archi sono stati presi in considerazione nel corso dell'algoritmo, e sia il primo $e$ il primo arco preso che non compare in T*. Se inserisco $e$ in T* si forma di certo un ciclo C. Il ciclo C contiente almeno un arco $e'$ che non appartiene a T (infatti non tutti gli archi presenti nel ciclo C sono presenti in T altrimenti $e$ non sarebbe stato preso dall'algoritmo di Kruskal). Consideriamo ora l'albero T' che ottengo da T* inserendo l'arco $e$ ed eliminando $e'$. Il costo del nuovo albero T' (che sarebbe $costo(T*)- costo(e')+costo(e)$) non può aumentare rispetto a quello di T* (perché $costo(e) \leq costo(e')$ ) ma allora T' è un altro albero di copertura ottimo che differisce da T in meno archi di quanto faccia di T* che contraddice l'ipotesi che T* differisce da T nel minor numero di archi
![[Pasted image 20250321115908.png]]
### Implementazione
>[!warning] Idee
>- Con un pre-processing ordino gli archi nella lista E cosicché scorrendo la lista ottengo di volta in volta l'arco di costo minimo in tempo O(1).
>- Verifico che l'arco (x, y) non formi ciclo in T controllando se y è raggiungibile da x in T

```Python
def kruskal(G):
	E = [(c, u, v) for u in G for v, c in G[u] if u < v]
E.sort()
T = [[] for _ in G]
for c,u,v in E:
	if not connessi(u, v, T):
		T[u].append(v)
		T[v].append(u)
return T

def connessi(u, v, T, visitati):
	def DFSr(a, b, T, visitati):
		visitati[a] = 1
		for z in T[a]:
			if z == b:
				return True
			if not visitati[z]:
				if DFSr(z, b, T, visitati):
				return True
		return False
visitati = [0] * len(T)
return DFSr(u, v, T, visitati)
```



