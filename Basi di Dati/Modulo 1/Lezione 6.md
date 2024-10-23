# Chiusura di un insieme di dipendenze funzionali
Introduciamo $F^A$
Ricordiamo che il nostro problema è calcolare l'insieme di dipendenze $F^+$ che viene soddisfatto da ogni istanza legale di uno schema R su cui è definito un insieme di dipendenze funzionali $F$.

Abbiamo concluso banalmente che F $\subseteq$ F+ in quanto una istanza è legale **solo se** soddisfa **tutte** le dipendenze in F.

Partiamo da un insieme diverso, "facile" da calcolare

Introduciamo $F^A$
>[!example] Assiomi di Armstrong
>Denotiamo con $F^A$ l'insieme di dipendenze funzionali definito nel modo seguente:
>- se $f \in F$ allora $f\in F^A$
>- se $Y\subseteq$ X $\subseteq R$ allora $X\to Y \in F^a$ (*assioma della riflessività*)
>- se $X\to Y \in F^A$ allora $XZ \to YZ \in F^A$, per ogni $Z \subseteq$ R (*Assioma dell'aumento*)
>- se $X \to Y \in F^A$ e $Y \to Z \in F^A$ allora $X \to Z \in F^A$(*assioma della transitività*)

**Dimostreremo che $F^+ = F^A$**, cioè che la chiusura di un isnieme di dipendenze funzionali F può essere ottenuta a partire da F applicando ricorsivamente gli *assiomi di Armstrong*.

>[!tip]
Se due insiemi hanno la stessa chiusura, e $F^+ = G^+$, esiste un insieme $G$ con le stesse chiusure di $F$. Allora un'istanza legale per $F$ sarà legale anche per $G^+$, quindi dire che due insiemi sono uguali vuol dire che contengono gli stessi elementi. Quindi due insiemi che hanno le stesse chiusure avranno le stesse istanze legali.

Dai tre assiomi si possono derivare tre regole che producono ancora elementi di $F^A$
>[!note]
>se $X \to Y \in F^A$ e $X \to Z \in F^A$ allora $X \to YZ \in F^A$(*regola dell'unione*)
>se $X \to Y \in F^A$ e $Z \subseteq Y$ allora $X \to Z \in F^A$ *(regola della decomposizione)*
>se $X \to Y \in F^A$ e $WY \to Z \in F^A$ allora $WX  \to Z \in F^A$   *(regola della pseudotransitività)*

Dimostrazioni

>[!warning] osservazione
>1) Per la regola dell'***unione***, se $X \to A_i \in F^A, i=1,...,n$ allora $X \to A_1,...,A_i,...,A_n \in F^A$
>2) Per la regola della ***decomposizione***, se $X \to A_1, ..., A_i, ..., A_n \in F^A$ allora $X \to A_i \in F^A, i=1,...,n$
>
>Quindi
>- $X \to A_1, ..., A_i, ..., A_n \in F^A \iff X \to A_i \in F^A, i=1,...,n$

>[!note] Lemma
>Siano R uno schema di relazione ed F un insieme di dipendenze funzionali su R. Si ha che:
>$X \to Y \in F^A \iff Y \subseteq X^+$
>**Dim**
>Sia $Y = A_1, A_2, ..., A_n.$
> *Parte se*
> Poiché $Y \subseteq X^+$, per ogni $ i,i =1,...,n$ si ha che $X \to A_i \in F^A.$
> Pertanto per la regola dell'unione, $X\to Y \in F^A$
> *Parte solo se*
> Poiché $X \to Y \in F^A$, per la regola della **decomposizione** si ha che, per ogni $i, i = 1,...,n$ e, quindi, $Y \subseteq X^+$

>[!example] Teorema: $F^+ = F^A$
> **Teorema** Siano R uno schema di relazione ed F un insieme di dipendenze funzionali su R. Si ha $F^+ = F^A$
> **Dim** 
> - (l'uguaglianza di insiemi si dimostra usando la *doppia inclusione*)
> - $F^+ \supseteq F^A$ Sia $X \to Y$ una dipendenza funzionale in $F^A$. Dimostriamo che $X \to Y \in F^+$ *per induzione* sul numero *i* di *applicazioni di uno degli assiomi di Armstrong*
> **Base dell'induzione**: $i = 0$. In tal caso $X \to Y$ è in $F$ e quindi, banalmente, $X \to Y$ è in $F^+$
> **Induzione**: $i = 0$. Per l'***ipotesi induttiva*** ogni dipendenza funzionale ottenuta a partire da $F$ applicando gli assiomi di Armstrong  un numero di volte **minore o uguale a -1** è in $F^+$. 
> 
> Dobbiamo dimostrarlo per un numero di volte uguale a ***i***. Si possono presentare tre casi:
> - $X \to Y$ è stata ottenuta mediante l'assioma della ***riflessività*** in tal caso $Y \subseteq X$. Sia r un'istanza di $R$ e siano $t_1$ e $t_2$ due tuple di $r$ tali che $t_1[X] = t_2[Y]$
> - $X \to Y$ è stata ottenuta applicando l'assioma dell'***aumento*** ad una dipendenza funzionale $V \to W$ in $F^A$, ottenuta a sua volta applicando ricorsivamente gli assiomi di Armstrong un numero di volte **minore o uguale a i-1** (quindi per *l'ipotesi induttiva $V \to W \in F^+$*); sarà quindi $X = VZ$ e $Y = WZ$ per qualche $Z \subseteq R$. 
>  Sia $r$ un'istanza legale di $R$ e siano $t_1$ e $t_2$ due tuple di $r$ tali che $t_1[X] = t_2[X]$; 
>  banalmente si ha che **$t_1[V] = t_2[V]$** e *$t_1[Z] = t_2[Z]$*. Per l'ipotesi induttiva da **$t_1[V] = t_2[V]$** segue ***$t_1[W] = t_2[W]$***; e da ***$t_1[W] = t_2[W]$*** segue  *$t_1[Z] = $t_2[Z]$*
>  - $X \to Y$ è stata ottenuta applicando l'assioma della transitività a due dipendenze funzionale $X \to Z$ e $Z \to Y$ in $F^A$, ottenute a loro volta applicando ricorsivamente gli assiomi di Armstrong un numero di volte minore o uguale a $i -1$(quindi per *l'ipotesi induttiva $X \to Z, Z \to Y \in F^+$*). Sia $r$ un'istanza *legale* di $R$ e siano $t_1,t_2$ due tuple di r tali che *$t_1[X] = t_2[X]$*. Per l'ipotesi innduttiva da *$t_1[X] = t_2[X]$* segue **$t_1[Z] = t_2[Z]$**; da **$t_1[Z] = t_2[Z]$** segue ***$t_1[Y] = t_2[Y]$***



## Ulteriore dimostrazione 
Consideriamo la seguente istanza $r$ di $R$
<table>
    <tr>
        <th colspan="2">X<sup>+</sup></th>
        <th colspan="6">R - X<sup>+</sup></th>
    </tr>
    <tr>
        <td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>...</td><td>1</td>
    </tr>
    <tr>
        <td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>...</td><td>0</td>
    </tr>
</table>

Dimostreremo che questa istanza è *legale*.
Utilizzando questa istanza dimostreremo che se  **$X \to Y \in F^+$** **avremo necessariamente** che $X \to Y \in F^A$.

Prendiamo una qualunque dipendenza $V \to W \in F$ e mostriamo per prima cosa che r è un' istanza legale:
>[!example] Dim
>Se $t_1[V] \neq t_2[V]$ ovvero se  $V \cap R-X^+ \neq \emptyset$  allora è **soddisfatta**.
>- Se $t_1[V] = t_2[V] \implies V \subseteq X^+$ (sappiamo che sono uguali sicuramente solo in $X^+$). Per il *lemma 1* sappiamo che $V \subseteq X^+ \implies X \to V \in F^A$ e per ***transitività*** insieme a $V \to W \in F \implies X \to W \in F^A \implies  W \subseteq X^+ \implies t_1[W] = t_2[W]$. Quindile due tuple sono uguali sia sui valori di $V$ che su quelli di $W$.
>
>***L'istanza è legale***


