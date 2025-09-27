# Liguaggi regolari
$REG = \{ L \subseteq \Sigma^{*} :\exists \text{ DFA M tale che } L(M)=L\}$
Questo rappresenta l'insieme dei linguaggi riconosciuti dal DFA M.

>[!warning] oss: 
>Non tutti i linguaggi sono regolari

Vogliamo capire come progettare DFA per un dato linguaggio.

>[!warning] oss:
> Ce ne può essere più di uno per un determinato linguaggio

>[!example] Example:
>$L=\{ x \in \{ 0,1 \}^{*} \ t.c. \ x = 1y, y \in \{ 0,1 \}^{*}  \}$
>![[Pasted image 20250927163943.png|350x250]]
>>[!warning] oss
>>Se $\delta$ non definita e non disegno lo stato pozzo (che in questo caso è $q_{2}$ va bene)

#### Prova di correttezza
- $DFA$ accetta $x \iff x \in L$
>[!warning] oss
>$$\begin{align}
>&\delta^{*}(q_{1},u)=q_{1} \ \forall u \in \{ 0,1 \}^{*}  \\
>&\delta^{*}(q_{2},u)=q_{2}\forall  
>\end{align}$$






