# Partizionamento della memoria
Uno dei primi metodi per la gestione della meoria. Antecedente all'introduzione della memoria virtuale, non viene più usata
>[!note] Partizionamento Fisso Uniforme
>Tutte le partizioni hanno una dimensione fissa ed è la medesima per tutte.  Se un processo ha una dimensione minore o uguale  a quella della partizione allora può essere caricato in una partizione libera.
>Il sistema operativo può far togliere un processo da una partizione
>>[!warning] Problemi
>>Un programma potrebbe non entrare in una partizione
>>Uso inefficiente della memoria, ogni programma, anche il più piccolo occupa un'intera partizione

>[!note] Partizionamento Fisso Variabile
>La dimensione è variabile, ma le partizioni sono fisse perché sono quelle decise all'inizio e non cambiano più. 
>>[!warning] Mitiga un pò i problemi ma non li risolve.

>[!note] Algoritmo di Posizionamento
>Partizioni di ugual lunghezza: algoritmo banale, non c'è scelta
>Partizioni di diversa lunghezza: un processo va nella partizione più piccola che può contenerlo, questo minimizza la quantità di spazio sprecato. Può esserci una coda per ogni partizione, oppure una per tutte

>[!note] Partizionamento Dinamico
>Le partizioni variano sia in misura che in quantità, per ciascun processo viene allocata esattamente la quantità di memoria che serve. *Frammentazione esterna*: la memoria che non è usata per nessun processo viene frammentata. Si può risolvere con la compattazione, il SO sposta i processi in modo tale che siano contigui, però ha un elevato overhead.
>Il SO deve decidere a quale blocco libero assegnare un processo.
>>[!tip] Algoritmo best-fit
>>Sceglie il blocco la cui misura è la più vicina a quella del processo da posizionare, nonostante l'apparenza ragionevole, è quello con risultati peggiori perché lascia frammenti molto piccoli e costringe a fare spesso la compattazione. (**il peggiore**)
>
>>[!tip] Algoritmo first-fit
>>Scorre la memoria dall'inizio; il primo blocco con abbastanza memoria viene subito scelto, molto veloce e tende a riempire solo la prima parte della memoria.(**il migliore**)
>In ogni caso il problema della compattazione rimane perché è tipico della partizione dinamica, cambia solo quanto frequentemente devo farla, per questo ad oggi nessuno di questi sistemi viene utilizzato.

