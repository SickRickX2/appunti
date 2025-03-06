Dato un grafo connesso G ed un intero *k* vogliamo sapere se è possibile colorare i nodi del grafo in modo che nodi adiacenti abbiano sempre colori distinti.
![[Pasted image 20250306172343.png]]
Il caso "peggiore" in cui si richiedono $\Theta (n)$ colori è quando abbiamo un grafo completo (ovvero ci sono tutti gli archi possibili).
>[!note] Requisiti per un grafo 2-colorabile
>Un grafo *2-colorabile* è un grafo che può essere colorato usando solamente due colori.
>Affinché ciò sia possibile è necessario e sufficiente che il grafo non contenga cicli di lunghezza dispari.
>>[!warning] Spiegazione
>>Un ciclo di lunghezza dispari rende impossibile la colorazione del grafo con due colori perché lungo il ciclo i colori devono necessariamente alternarsi.

>[!note] Algoritmo di bi-colorazione
>L'algoritmo di bi-colorazione che segue prova che un *grafo senza cicli dispari* può sempre essere 2-colorato.
>- colora il nodo 0
>- effettua una visita in profondità del grafo a partire dal nodo 0.  Nel corso della visita, a ciascun nodo x che incontri assegna uno dei due colori 0 e 1. Scegli il colore da assegnare in modo che sia diverso dal colore assegnato al nodo padre che ti ha portato a visitare x
>**La prova di correttezza:** Siano x  e y due nodi adiacenti in G, consideriamo i due possibili casi e facciamo vedere che in entrambi i casi i due nodi al termine avranno colori opposti.
>1) *l'arco (x,y) viene attraversato durante la visita.* In questo caso banalmetne i due nodi hanno colori distinti.
>2) l'arco (x,y ) NON viene attraversato durante la visita. Sia x il nodo visitato prima. Esiste un cammino in G che da x porta a y ( quello seguito dalla visita), questo cammino si chiude formando un ciclo con l'arco (y,x). Il ciclo è di lunghezza pari per ipotesi, quindi il cammino è di lunghezza dispari. Poiché sul cammino i colori si alternano il primo nodo (x) e l'ultimo nodo (y) del cammino avranno colori diversi.

>[!example] Algoritmo per bicolorare
>```Python
>def Colora(G):
>	def DFSr(x, G, Colore, c):
>	Colore[x] = c
>	for y in G[x]:
>	
>
>
>```



