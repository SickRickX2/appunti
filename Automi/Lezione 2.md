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
>&\delta^{*}(q_{2},u)=q_{2}\forall u \in \{ 0,1 \}^{*}  
>\end{align}$$

*Dimostriamo per induzione* 
$x \in L \iff DFA \text{ accetta} \ x$
**base:** $|x| = 0$ Se $x=\epsilon$, $\delta^{*}(q_{0},\epsilon)=\delta(q_{0},\epsilon)$
**passo induttivo:** Sia $n> 0$ supponiamo che $|w| \leq n$
$$\delta^{*}(q_{0},w)=\begin{cases}
&q_{1} \text{ se } \ w \text{ inizia con 1} \\ \\
&q_{2} \text{ se } \ w \text{ inizia con 0} \\ \\  
&q_{0} \text{ se } w=\epsilon
\end{cases}
$$
Prendo $x$ t.c. $|x|=n+1$ e lo penso $x=au$ con $a \in \{ 0,1 \}$ e $u \in \{ 0,1 \}^{n}$.







