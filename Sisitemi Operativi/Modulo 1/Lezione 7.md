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
