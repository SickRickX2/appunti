>[!note] ## Translation Lookaside Buffer
>TLB; letteralmenete memoria temporanea per la traduzione futura.
>Ogni riferimento alla memoria virtuale può generare due accessi alla memoria:
>- uno per la tabella delle pagine
>- uno per prendere il dato
>Si usa una cache veloce per gli elementi delle tabelle delle pagine (proprio il TLB che contiene gli elementi delle tabelle delle pagine che sono stati usati più volte)

>[!example] ### Come funziona 
Dato un indirizzo virtuale, il processore esamina dapprima il TLB. Se la pagina è presente si prende il frame number e si ricava l'indirizzo reale. Altrimenti si prende la normale tabella delle pagine del processo. Se la pagina risulta in memoria principale a posto, altrimenti si gestisce il page fault come descritto prima. Dopodiché il TLB viene aggiornato includendo la pagina appena acceduta.
>![[Pasted image 20241025151022.png]]

Il sistema operativo deve poter resettare il TLB, è la soluzione peggiore dal punto di vista delle prestazioni. Per far almeno un pò meglio alcuni processori permettono di etichetare con il PID ciascuna entry del TLB oppure di invalida