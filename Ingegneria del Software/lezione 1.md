## Modelli
### Markov Chains
Una markov chain $M=(S,p)$ è descritta come un insieme di **stati** $S$ e la *probabilità di transizione* $p: S \times S \to [0,1]$ è tale che $p(s'|s)$ è la probabilità di transizione dallo stato $s'$ allo stato $s$ .
>[!note] Probabilità di Transizione
>La probabilità di transizione è definita come:
>$\forall s \in S$   $\sum_{s'\in S}\ \ p(s'|s)=1$

Una *Markov Chain* (o Markov process) è caratterizzato dalla 