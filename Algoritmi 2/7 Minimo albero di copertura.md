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

