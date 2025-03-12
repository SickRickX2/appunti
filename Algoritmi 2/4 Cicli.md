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

