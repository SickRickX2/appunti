>[!note] ## Translation Lookaside Buffer
>TLB; letteralmenete memoria temporanea per la traduzione futura.
>Ogni riferimento alla memoria virtuale può generare due accessi alla memoria:
>- uno per la tabella delle pagine
>- uno per prendere il dato
>Si usa una cache veloce per gli elementi delle tabelle delle pagine (proprio il TLB che contiene gli elementi delle tabelle delle pagine che sono stati usati più volte)
