Dato un grafo *G* diretto o indiretto ed un suo nodo *u*, vogliamo sapere se da *u* è possibile raggiungere un ciclo in G.
>[!warning] Idea di partenza (sbagliata)
>Visita il grafo e se nel corso della visita incontri un nodo già visitato interrompila e restituisci True, se al contrario la visita termina regolarmente restituisci False
>>[!note] Codice
>>```Python
>>def ciclo(u, G):
>>	visitati = [0] * len(G)
>>	return DFSr(u, G, visitati)
>>		def DFSr(u, G, )
>>```