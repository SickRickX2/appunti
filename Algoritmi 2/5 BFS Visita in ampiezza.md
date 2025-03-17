>[!note] Distanza minima
>Dati due nodi $a$ e $b$ di un grafo $G$, definiamo *distanza minima* il numero minimo di archi che bisogna attraversare per raggiungere $b$ a partire da $a$. La distanza è posta a $+ \infty$ se $b$ non è raggiungibile partendo da $a$.
>![[Pasted image 20250317095608.png]]

>[!danger] Problema
>Dato un grafo $G$ ed un suo nodo x vogliamo conoscere le distanze di tutti i nodi di $G$ da $x$.

La *visita in ampiezza (Breadth First Search)* esplora i nodi del grafo da quelli a distanza 1 dalla sorgente $s$. Poi visita quelli a distanza 2 e così via. L'algoritmo visita tutti i vertici a livello $k$ prima di passare a quelli a livello $k+1$ 


