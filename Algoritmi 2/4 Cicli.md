Dato un grafo *G* diretto o indiretto ed un suo nodo *u*, vogliamo sapere se da *u* è possibile raggiungere un ciclo in G.
>[!warning] Idea di partenza (sbagliata)
>Visita il grafo e se nel corso della visita incontri un nodo già visitato interrompila e restituisci True, se al contrario la visita termina regolarmente restituisci False
>>[!note] Codice
>>```Python
>>def ciclo(u, G):
>>	visitati = [0] * len(G)
>>	return DFSr(u, G, visitati)
>>	
>>		def DFSr(u, G, visitati) :
>>			visitati[u] == 1
>>			for v in G[u]:
>>				if visitati[v] == 1:
>>					return True
>>				if DFSr(v, G, visitati):
>>					return True
>>			return False
>>```

>[!danger] Il codice è scorretto nel caso di grafi non diretti
>Il codice è sbagliato perché (per come è codificato il grafo non diretto) se x ha un arco che lo collega a  y nella lista di adiacenza di x è presente y e nella lista di adiacenza di y è presente x. Questo viene interpretato erroneamente come un ciclo di lunghezza 2. (**La procedura proposta termina quindi sempre con True**)

Per risolvere il problema, durante la visita del ciclo, devo distinguere nella lista di adiacenza di ciascun nodo y che incontro il nodo x che mi ha portato a visitarlo, ovvero devo **tenere traccia dei padri**

```Python
def ciclo(u ,G):
	visitati = [0] * len(G)
	return DFSr(u, u, G, visitati)

	def DFSr(u, padre, G, visitati):
		visitati[u] = 1
		for v in G[u]:
			if visitati[1] == 1:
				if v != padre:
					return True
			else:
				if DFSr(v , u, G, visitati):
				return True
		return False
	
```
>[!tip] Spiegazione
>Questo codice restituisce True se nella visita da u si incontra un nodo già visitato diverso dal padre, False altrimenti.
>Ogni nodo deve sapere chi è suo padre altrimenti il codice non funziona.

>[!tip] Complessità
>La complessità di questo algoritmo è $O(n)$, questo costo è dovuto al fatto che se il grafo
