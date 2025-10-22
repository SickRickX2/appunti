# L'avvento dei big data
Non usiamo più i dispositivi per esigenze specifiche ma per uso personale.
Il dato è esso stesso informazione.
Con l'IA cambia il fatto che non soltanto la conoscenza rappresenta il mondo, perché la conoscenza assume un ruolo attivo. Da copia della realtà diventa un elemento di trasformazione della realtà, genera e produce conoscenza al di là di ciò che ha imparato.

L'output non è mai grezzo ma adattato a certe esigenze matematiche.
Abbiamo i due strati sottostanti e i neuroni. Le parole vengono scomposte in token e ogni token viene trasformato in token embedding, ogni volta che diventa embedding ha circa 760 dimensioni. I token sono tutti diversi ma con la stessa dimensione.

Ciascuna parola ha un peso, questo si chiama *embedding astratto*. I token vengono conformati ciascuno al loro peso

Categorie di funzioni che una dimensione può codificare:
- *funzioni sintattiche*
- *funzioni semantiche*
- *funzioni contestuali e pragmatiche*
Dentro ogni dimensione c'è un neurone, recupera i valori che formano ciascuna dimensione. Abbiamo tante dimensioni quanti neuroni. Per questo vengono chiamati anche **embedding di attivazione**.

Proiezioni lineari, sono dei vettori:
- key
- query
- value

>[!note] BIAS
>A volte un token conta poco, quindi rischia di non essere processato. Quindi si aggiunge un peso artificiale per essere considerato. Ma il numero totale degli embedding devono rimanere uguali, quindi se aggiungo da una parte tolgo da un'altra. 

Può succedere che un embedding ecceda dalle sue dimensioni quindi bisogna applicare un processo di *normalizzazione*. Trasformando da multidimensionale ad una monodimensionale in modo da poter fare delle operazioni lineari su numeri grazie a questa compressione


