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
>$X \to Y \in F^A$
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




