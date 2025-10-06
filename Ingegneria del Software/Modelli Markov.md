## Modelli
### Markov Chains
Una markov chain $M=(S,p)$ è descritta come un insieme di **stati** $S$ e la *probabilità di transizione* $p: S \times S \to [0,1]$ è tale che $p(s'|s)$ è la probabilità di transizione dallo stato $s'$ allo stato $s$ .
>[!note] Probabilità di Transizione
>La probabilità di transizione è definita come:
>Equazione 1
>$\forall s \in S$   $\sum_{s'\in S}\ \ p(s'|s)=1$

Una *Markov Chain* (o Markov process) è caratterizzato dalla **assenza di memoria**, vale a dire che le previsioni possono essere fatte solo considerando lo stato presente e non sono influenzate da quelli passati.

![[Pasted image 20251006101335.png]]

>[!example] Example: 
>Si la markov chain con $S=\{\text{rainy,sunny}\}$
>![[Pasted image 20251006101509.png|200x100]]

Se una Markov chain $M$ *transiziona* a passi di **tempo discreti**(cioè i time steps $t_{0},t_{1},t_{2}$... sono numerabili) e  
lo **spazio degli stati** è numerabile, allora è chiamato un *DTMC (Discrete-Time Markov Chain)*. Ci sono anche altre classificazioni per spazi degli stati continui e tempi continui.

Il Markov process è caratterizzato da una**matrice di transizione** la quale descrive la probabilità di certe transizioni, come nell'esempio precedente. Vedremo più avanti che implementare queste matrici in $\text{C++}$ è molto semplice con la libreria ```<random>``` 
### Markov decision process
Un *Markov Decision Process (MDP)*, anche se ne condivide il nome, è **diverso** da una Markov Chain, perché interagisce con **l'ambiente esterno**. Un MDP $M$ è una tupla $I,O,S,p,g$ definita nel seguente modo:
- $I$ è un insieme di *valori di input*
- $O$ è un insieme di *valori di output*
- S è un insieme di *stati*
- $p:S \times S \times I \to [0,1]$ è tale che $p(s'|s,i)$ è la probabilità di passare allo stato $s'$ dallo stato $s$ quando il **valore di input** è $i$
- $g: S \to O$ è la *funzione di output*
- $s_{0} \in S$ è lo *stato iniziale*

Lo stesso vincolo nell'Equazione 1 vale anche per i MDP, con una differenza importante: **per ogni valore di input**, la somma delle probabilità di transizione **per quel valore** di input deve essere 1.
$\forall s \in S \ \forall i \in I  \ \sum_{s' \in S} p(s'|s,i) = 1$

>[!example] Example: esempio di MDP
>Il processo di sviluppo di una compagnia può essere modellato come un MDP
>$MDP = (I,O,S,p,g)$ definito come
>- $I =\{ \epsilon \}^{1}, O  \ Cost \times Duration,S = \{ 0,1,2,3,4 \},s_{0}=0$
>$$
> g = \begin{cases}
>&(0,0) \ s \in \{ 0,4 \} \\
>&(20000,2) \ s \in \{ 1,3 \} \\
>&(4000,4) \ s=2
\end{cases}
>$$
>![[Pasted image 20251006121421.png]]






