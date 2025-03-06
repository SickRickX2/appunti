Dato un grafo connesso G ed un intero *k* vogliamo sapere se è possibile colorare i nodi del grafo in modo che nodi adiacenti abbiano sempre colori distinti.
![[Pasted image 20250306172343.png]]
Il caso "peggiore" in cui si richiedono $\Theta (n)$ colori è quando abbiamo un grafo completo (ovvero ci sono tutti gli archi possibili).
>[!note] Requisiti per un grafo 2-colorabile
>Un grafo *2-colorabile* è un grafo che può essere colorato usando solamente due colori.
>Affinché ciò sia possibile è necessario e sufficiente che il grafo non contenga cicli di lunghezza dispari.
>>[!warning] Spiegazione
>>Un ciclo di lunghezza dispari rende impossibile la colorazione del grafo con due colori perché lungo il ciclo i colori devono necessariamente alternarsi.

