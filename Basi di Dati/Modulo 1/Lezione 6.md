# Chiusura di un insieme di dipendenze funzionali
Introduciamo F^A
Ricordiamo che il nostro problema è calcolare l'insieme di dipendenze F+ che viene soddisfatto da ogni istanza legale di uno schema R su cui è definito un insieme di dipendenze funzionali F

Abbiamo concluso banalmente che F $\subset$ F+ in quanto una istanza è legale **solo se** soddisfa **tutte** le dipendenze in F.

Partiamo da un insieme diverso, "facile" da calcolare

Introduciamo F^A
>[!example] Assiomi di Armstrong
>Denotiamo con F^A l'insieme di dipendenze funzionali definito nel modo seguente:
>- se f $\in$ F allora f$\in$ F^A
>- se Y$\subset$ X $\subset$R allora X$\to$ Y $\in$F^a (*assioma della riflessività*)
>- se X$\to$ Y $\in$ F^A allora XZ $\to$ YZ $\in$ F^A, per ogni Z $\subset$ R
>- se X $\to$ Y $\in$ F^A e Y $\to$ Z $\in
