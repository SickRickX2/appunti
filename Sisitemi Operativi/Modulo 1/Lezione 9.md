>[!note] ## Translation Lookaside Buffer
>TLB; letteralmenete memoria temporanea per la traduzione futura.
>Ogni riferimento alla memoria virtuale può generare due accessi alla memoria:
>- uno per la tabella delle pagine
>- uno per prendere il dato
>Si usa una cache veloce per gli elementi delle tabelle delle pagine (proprio il TLB che contiene gli elementi delle tabelle delle pagine che sono stati usati più volte)

>[!example] ### Come funziona 
Dato un indirizzo virtuale, il processore esamina dapprima il TLB. Se la pagina è presente si prende il frame number e si ricava l'indirizzo reale. Altrimenti si prende la normale tabella delle pagine del processo. Se la pagina risulta in memoria principale a posto, altrimenti si gestisce il page fault come descritto prima. Dopodiché il TLB viene aggiornato includendo la pagina appena acceduta.
>![[Pasted image 20241025151022.png]]

Il sistema operativo ogni volta che cambiamo processo deve poter resettare il TLB, è la soluzione peggiore dal punto di vista delle prestazioni. Per far almeno un pò meglio alcuni processori permettono di etichetare con il PID ciascuna entry del TLB oppure di invalidare solo alcune parti del TLB. E' comunque necessario anche senza TLB dire al processore dov'è la nuova tabella delle apgine 

>[!note] Mapping Associativo
>Il TLB contiene solo alcuni elementi tratti dalle tabelle delle pagine, il numero della pagina non può essere usato direttamente come indice per il TLB.  Il SO può interrogare più elementi del TLB contemporaneamente per capire se c'è o no una hit.
>- Altro problema: bisogna fare in modo che il TLB contenga solo pagine in **RAM.** 

## Segmentazione
Permette al programmatore di vedere la memoria come un insieme di spazi di indirizzi. La dimensione degli indirizzi è variabile. L'importante è che permette di condividere dati e allo stesso tempo proteggerli.

Ogni processo ha una sua tabella dei segmenti (come per le pagine)

>[!note] Paginazione e Segmentazione 
>La paginazione è "trasparente" al programmatore nel senso che il programmatore, questo vale  anche per il compilatore, non ne è a conoscenza
>Mentre la segmentazione è visibile al programmatore, ovviamente se programma in  assembler  altrimenti ci pensa il compilatore


