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
$\delta^{*}(q_{0},a)=\delta(q_{0},au)=\delta^{*}(\delta(q_{0},a),u)$ 
$(q_{0},a)=q_{2} \text{ se } a=0$ 
$(q_{0},a)=q_{1} \text{ se } a=1$ 
Poiché abbiamo dimostrato prima che se ci arriva rimane sempre in $q_{1}$ e in $q_{2}$ e allora il DFA $\iff a=1$

### Operazioni sui linguaggi
Fissiamo $\Sigma=\{ 0,1 \}$. per $n \in \mathbb{N}$. $[n]=\{ 1,2,\dots n \}$
Siccome i linsguaggi sono insieme di stringhe allora posso considerare su di essi per le operazioni:
- *Unione*: $L_{1}\cup L_{2}=\{x \in \Sigma^{*}:x \in L_{1} \vee x \in L_{2} \}$
- *Interazione*:  $L_{1}\cap L_{2}=\{x \in \Sigma^{*}:x \in L_{1} \vee x \in L_{2} \}$
- *Complimento*: $\neg L_{1}=\{ x \in \Sigma^{*}:x \not\in L \}$
- ***Concatenazione***: Se abbiamo $x=a_{1},\dots,a_{n}$ e $y=b_{1}\dots b_{n}$ con $n,m>0$ $$
\begin{cases}
&x\epsilon = x \\
&x(ya)=(xy)a \\ x,y \in \Sigma^{*} \\
a\in\Sigma
\end{cases}
$$
Posso concantenare i inguaggi:
$L_{1} \circ L_{2}=\{ xy:x \in L_{1} \ e \ y\in L_{2} \}$
>[!example] Example:
>$$
>\begin{align}
>&\Sigma = \{ a,b \} \\
>&L_{1}=\{ a,ab,ba \} \\
>&L_{2}=\{ ab,b \} \\ \\
>\end{align}
>$$
>$L_{1} \circ L_{2}= \{ aab,ab,abab,abb,baab,bab \}$

- *Potenza*: la potenza è un caso speciale di concatenazione.
Per le stringhe $x^{n}=x\dots x \ n\text{ volte } x \in \Sigma^{*}$
$$
\begin{cases}
&x^{0} = \epsilon \\
&x^{n+1}=x^{n} \cdot x
\end{cases}
$$
Lo stesso vale per i linguaggi
$$
\begin{cases}
&L^{0} = \epsilon \\
&L^{n+1}=L^{n} \circ L
\end{cases}
$$
Quindi la $*$ :
$L^{*}=  L^{n}= \bigcup_{n\geq_{0}} \epsilon \cup L^{1}\cup L^{2}\cup L^{n}$
#### Chiusura dei linguaggi regolari
Vogliamo studiare la proprietà della chiusura dei linguaggi regolari
Ovvero:
Se $L_{1},L_{2} \in REG$ posso dire che $L_{1}\cup L_{2},L_{1}\cap L_{2},\neg L_{1},L^{*}$ sono regolari?
>[!note] Teorema 1
>REG è chiusa per *unione*.
>**Intuizione**: $L_{1},L_{2} \in REG$ ovvero $\exists M_{1},M_{2}\text{ DFA t.c. }$
>$L(M_{1})=L_{1}$ e $L(M_{2})=L_{2}$
>Devo definire M t.c $L(M)=L_{1}\cup L_{2}$
>*Problema:* Dato x candidato non posso prima provare a vedere se $M_{1}(x)$ accetta? No!! M deve eseguire $M_{1}$ e $M_{2}$ in parallelo e accettare se e solo se uno dei due accetta


 

