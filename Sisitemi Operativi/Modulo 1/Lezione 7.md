# Partizionamento della memoria
Uno dei primi metodi per la gestione della meoria. Antecedente all'introduzione della memoria virtuale, non viene più usata
>[!note] Partizionamento Fisso Uniforme
>Tutte le partizioni hanno una dimensione fissa ed è la medesima per tutte.  Se un processo ha una dimensione minore o uguale  a quella della partizione allora può essere caricato in una partizione libera.
>Il sistema operativo può far togliere un processo da una partizione
>>[!warning] Problemi
>>Un programma potrebbe non entrare in una partizione
>>Uso inefficiente della memoria, ogni programma, anche il più piccolo occupa un'intera partizione

>[!note] Partizionamento Fisso Variabile
>La dimensione è variabile 