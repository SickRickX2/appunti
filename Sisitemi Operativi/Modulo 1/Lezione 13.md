#### La gestione dello spazio libero
La gestione dello spazio libero è altrettanto importante di qullo occupato. Per allocare spazio per i file, occorre sapere dov'è lo spazio libero (non si può fare guardando la tabella di allocazione). Serve una tabella di allocazione di disco oltre  a quella di allocazione per i file. Ogni volta che si alloca o si cancella un file, lo spazio libero va aggiornato.
>[!note] Tabelle di Bit
>Vettore con un bit per ogni blocco su disco(0 = libero,1 = occupato). Va bene per tutti gli schemi visti fino ad ora. Minimizza lo spazio richiesto alla tabella di allocazione del disco. Se il disco è quasi pieno, la ricerca di uno spazio libero può richiedere molto tempo, risolvibile con tabelle riassuntive di porzioni della tabella di bit.

