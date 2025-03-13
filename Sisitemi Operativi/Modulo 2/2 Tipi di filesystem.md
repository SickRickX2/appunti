Il filesystem root(/) contiene elementi eterogenei
- Disco interno solido o magnetico
- Filesystem su disco esterno (usb)
- Filesystem di rete
- Filesystem virtuali (usati dal kernel per gestire risorse)
- Filesystem in memoria principale

Tutto questo è possibile grazie al meccanismo del *mounting*

>[!note] mounting
>Una qualsiasi directory D dell'albero gerarchico può diventare il punto di mount per un altro (nuovo) filesystem F se e solo se la directory root di F diventa accessibile da D.
>- se D è vuota, dopo il mount conterrà F
>- se D non è vuota, dopo il mount conterrà F ma ciò non significa che i file all'interno di D sono andati persi ma diventeranno di nuovo accessibili dopo l'unmount di F.

>[!note] Partizioni
>Un singolo disco può essre suddiviso in due o più partizioni. Una partizione **A** può contenere il sistema