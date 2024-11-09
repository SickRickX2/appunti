## Terza forma normale
>[!note] Definizione
>Dati uno schema di relazione R e un insieme di dipendenze funzionali F su R, R è in terza forma normale se:
>***$\forall X \to A \in F^+, A \notin X$***
>- A **appartiene ad una chiave** *(è primo)*
>oppure
>- X **contiene una chiave** *(è superchiave)*

>[!warning] Attenzione
>Per quanto detto è sbagliato scrivere$X \to A \in F$ ,perchè non sapremmo se e come valutare una dipendenza del tipo $X \to AB$ (due o più attributi a destra )
