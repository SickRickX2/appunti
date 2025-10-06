## Modelli
### Markov Chains
Una markov chain $M=(S,p)$ è descritta come un insieme di **stati** $S$ e la *probabilità di transizione* $p: S \times S \to [0,1]$ è tale che $p(s'|s)$ è la probabilità di transizione dallo stato $s'$ allo stato $s$ .
>[!note] Probabilità di Transizione
>La probabilità di transizione è definita come:
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
- $I$ è un insieme di *input*
- $O$ è un insieme di out
