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

La posso *estendere* 



