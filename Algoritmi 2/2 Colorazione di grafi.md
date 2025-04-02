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
>
>**La prova di correttezza:** Siano x  e y due nodi adiacenti in G, consideriamo i due possibili casi e facciamo vedere che in entrambi i casi i due nodi al termine avranno colori opposti.
>1) *l'arco (x,y) viene attraversato durante la visita.* In questo caso banalmetne i due nodi hanno colori distinti.
>2) l'arco (x,y ) NON viene attraversato durante la visita. Sia x il nodo visitato prima. Esiste un cammino in G che da x porta a y ( quello seguito dalla visita), questo cammino si chiude formando un ciclo con l'arco (y,x). Il ciclo è di lunghezza pari per ipotesi, quindi il cammino è di lunghezza dispari. Poiché sul cammino i colori si alternano il primo nodo (x) e l'ultimo nodo (y) del cammino avranno colori diversi.

>[!example] Algoritmo per bicolorare
>```Python
>def Colora(G):
>	def DFSr(x, G, Colore, c):
>		Colore[x] = c
>		for y in G[x]:
>			if Colore[y] == -1:
>			 DFSr (y, G Colore 1-c)
>	
>	Colore = [-1] * len(G)
>	DFSr(0, G, Colore, o)
>	return Colore
>```
>>[!danger] Attenzione
>>Se il grafo G contiene cicli dispari l'algoritmo produce un assegnamento di colori sbagliato, per questo motivo esiste un algoritmo leggermente diverso che risolve questo problema

Nella versione che segue l'algoritmo produce una bi-colorazione se il grafo G è bi-colorabile mentre ritorna una lista vuota in caso contrario
```Python
def Colora1(G):
	Colore[x] = c
	for y in G[x]:
		if Colore[y] == -1:
			if not DFSr(y, G, Colore, 1-c):
				return False
		elif Colore[y] == Colore[x]:
			return False
	return True
	
	Colore = [-1] * len(G)
	if DFSr(0, G, Colore, 0):
		return Colore
	return []
	
```
La complessità dell'algoritmo per testare se un grafo è bicolorabile è quella di una semplice visita del grafo connesso da colorare:
$O(n+m)=O(m)$

## Connessioni
>[!note] Componente Connessa
>Una *componente connessa* ( o semplicemente una componente) di un grafo (indiretto) è un sottografo composto da un *insieme massimale* di nodi connessi da cammini.
>Un grafo si dice *connesso* se ha una sola componente connessa.
>![[Pasted image 20250306190656.png]]
>Vogliamo calcolare il *vettore C delle componenti connesse* di un grafo G. Vale a dire il vettore C che ha tanti elementi quanti sono i nodi del grafo e C[u] = C[v] se  e solo se u e v sono nella stessa componente connessa.
>![[Pasted image 20250306191209.png]]
>Se ho fatto n visite per esplorare il grafo, nel vettore troverò n valori che equivale a dire n componenti (n numero non i nodi). 
### Algoritmo
```Python
def Componenti(G):
	def DFSr(x, G, C, c):
		C[x] = c
		for y in G[x]:
			if C[y] == 0:
				DFSr(y, G, C, c)

###
	C = [0]*len(G)
	c = 0
	for x in range(len(G)):
		if C[x] == 0:
		c += 1
		DFSr(x, G, C, c)
	return C
```

![[Pasted image 20250307101204.png|200]]
La complessità di questo algoritmo è $O(n + m)$.
>[!tip] Spiegazione algoritmo
>Se faccio più di una visita non percorrerò mai archi o nodi già visitati. Quindi visito ogni volta partizoni e in totale tutto il grafo, ovvero $O(n+m)$






 




