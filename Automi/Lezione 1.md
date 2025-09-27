1° modello: **Automi a stati finiti non deterministici**.
Ha 2 caratteristiche:
- memoria limitata
- processa i dati in maniera semplice (bit a bit in maniera sequenziale)

>[!example] Example: dispositivo apertura porta automatica
>Guardare libro

>[!note] Linguaggi
>Insieme di stringhe dove ci sono pattern riconoscibili. L'automa determina se l'input è in un linguaggio o meno.

>[!note] Stati
>Gli stati si chiamano q. Uno *Stato di accettazione* se termina su uno di questi stati allora l'automa **decide**. Un automa è una tupla composta da:
>- $\Sigma$ = alfabeto input
>- $Q$ = insieme di dati
>- $\delta$ = funzione che prende stato e carattere e porta in un altro stato tramite transizione

>[!example] Example: **DFA** precedente
>Ha come linguaggio delle stringhe w : w contiene almeno un 1 e numero pari di 0 che segue almeno un 1.

>[!note] Funzione di Transizione Estesa
>Per definire precisamente il linguaggio introduco la *funzione di transizione estesa*
>$\delta:Q \times \Sigma^{*}\implies Q$
>>[!warning] oss $\epsilon$ = stringa vuota
>
>$$
>\begin{cases}
>\delta^{*}(q,\epsilon) = \delta(q,\epsilon)\\
>\delta^{*}(q,ax)=\delta^{*}(\delta(q,a),x)
>\end{cases}
>
>$$
>$x,a\in\Sigma$

>[!note] Configurazione
>Altro concetto è la *configurazione* è coppia in $Q\times\Sigma^{*}$ 
>Dato $x \in \Sigma$ la configurazione *iniziale* è $(q_{0},x)$

**Passo di computazione**: porta da una configurazione ad un'altra
### Relazione Binaria
$$
(p,ax) \vdash_{M} (q,x) \iff \delta(p,a)=q 
$$
dove $p,q\in Q,a\in\Sigma,x \in \Sigma^{*}$.

La posso *estendere* ($\vdash_{M^{*}}$) considerando la *Chiusura Riflessiva e Transitiva*.
$$
\begin{align}
&(q,x)\vdash_{M}(q,x)\\
&(q,x)\vdash_{M}(p,by) \text{ e } (p,by)\vdash_{M}(r,y)\\ \\
&q,p,r\in Q \\
&a,b \in \Sigma, y\in \Sigma^{*} \\
\end{align}
$$
>[!note] Linguaggio Accettato
>Diciamo che $x  \in \Sigma^{*}$ è accettato da $M=(Q,\Sigma,\delta,q_{0},F)$ se $\delta^{*}(q_{0},x)\in F$
>oppure
>$(q_{0},x)\vdash_{M^{*}}(q,\epsilon)\in F$
>In altre parole $L(M)={x \in }$




