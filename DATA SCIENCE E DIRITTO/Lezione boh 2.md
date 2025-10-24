Si è invertito il rapporto tra uomo e macchina, il rapporto tra soggetto conoscente e oggetto conosciuto.

>[!note] ChatGPT
>Ci deve interessare la struttura interna; da dove passa la sua conoscenza.
>Composto da strati, neuroni e moduli. 
>Ogni strato ha uno strato sottostante. Il primo strato meccanismo di attenzione mentre il secondo una rete 

**Meccanismo di attenzione**
All'interno degli strati troviamo i neuroni che sono le dimensioni di ciascun vettore, ogni vettore ha diverse dimensioni ciascuna con una specifica funzione.

>[!tip] Vettore
>Quando l'input entra nel modello diventa un token (una parola diventa un numero o un pezzo di parola)

Un neurone si specializza rispetto agli altri, visto che hanno dei significati a sè che vengono riferiti in tutti gli altri token. Tutto questo in fase di progettazione
ad esempio il peso della parola francesco in relazione alla parola figma.

Dentro al primo stato ci sono 3 matrici con lo scopo di configurare i neuroni dei token in modo particolare. Sono 3 proiezioni lineari del token, ognuna con una dimensione a sè:
- key 
- query
- value
Key e value sono più a stretto contatto. Key e value sono le proiezioini che danno mentre query quella che chiede.
>[!note] Key
>Configura i neuroni del vettore in modo da evidenziare i numeri che rappresentano le loro caratteristiche principali

query se sollecitato da un token mostra il valore key se poi è soddisfacente prendono le informazioni all'interno di query. L'interazione di queste tre componenti crea un token temporaneo come risposta.

Ciò che avviene nella rete neurale dopo l'elaborazione nello strato di sopra è che bisogna mutare di nuovo il token attraverso operazioni non lineari.

Il token rimane fisso -> si crea token provvisorio -> scende nel sottostrato neurale -> moduli/funzioni *gelo* lavora sul token provvisorio per sistemarlo e che il numero dei neuroni sia sempre quello compattando o cambiando le dimensioni (bias).


Prevedere e volere -> se corrisponde ad una normale legale allora quello è dolo 

La norma prevede in astratto *fatto tipico* -> insieme di elementi per commettere un reato. In sostanza è una condotta astratta dove la causa di questa condotta è il soggetto, presuppone sia conseguenza di un azione di un soggetto. I reati sono fatti tipici commessi dall' **UOMO**
Ciò che la persona fa invece è *fatto storico*
