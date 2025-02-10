I tipi generici in Java sono un potente meccanismo che permette di scrivere codice flessibile e riutilizzabile; dando la possibilità di definire classi, interfacce e metodi che operano su tipi di dati specificati solo al momento dell'utilizzo.

Ad esempio le collezioni sono classi generiche do ve il tipo su cui operano è definito soltanto al mometno dell'istanziamento attraverso l'*operatore diamante* <>. Questo ha permesso di utilizzare un singolo codice per creare delle collection per qualsiasi tipo, ad esempio senza i tipi generici si sarebbe dovuto definire un tipo specifico di ArrayList per ogni tipo d'oggetto esistente.

>[!danger] Implementazione dei Tipi Generici
>I tipi generici sono implementati attraverso la cancellazione del tipo.

## Limiti
>[!note] No Primitivi
>Non è possibile utilizzare i tipi primitivi con tipi generici, questo perché durante la cancellazione del tipo, il tipo generico viene sostituito con Object e i primitivi non possono essere trattati come oggetti.

>[!note] No ereditarietà dei tipi generici
>Per le classi generiche non vale l'ereditarietà dei tipi generici 

>[!note] No upcasting
>Non è permesso l'upcasting nei tipi generici, ad esempio
>
