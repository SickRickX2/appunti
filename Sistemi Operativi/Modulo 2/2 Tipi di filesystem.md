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
>Un singolo disco può essre suddiviso in due o più partizioni. Una partizione **A** può contenere il sistema operativo e la partizione **B** i dati degli utenti (home directory degli utenti).

>[!tip] File *passwd* e *group*
>Rappresentano una delle filosofie di Linux, usare file di testo (con codifica ACII a 8 bit) con una struttura definita e conosciuta dai programmi che devono interagire con quei file.
>Sono file organizzati per righe ogni riga contiene vari campi separati da "*:*".
>Struttura:
>- *passwd* = username:password:uid:gid:gecos:homedir:shell
>	al posto della password si vedrà a schermo una *x* a causa della cifratura
>- *group* = password:groupID:lista utenti
>	Gli utenti nella Lista utenti sono separati da "*,*". Anche qui la password non viene visualizzata


>[!note] I file
>Ogni file nel filesystem è rappresentato da una struttra dati *inode* ed è univocamente identificato da un *inode number*.
>La cancellazione di un file libera l'*inode number* che verrà riutilizzato quando necessario per un nuovo file.
>>[!tip] Struttura dati inode
>>- Type: indica il tipo di file
>>- User ID: ID del proprietario del file
>>- Group ID: id del gruppo a cui è associato il file
>>- Mode: Permessi (read, write, exec) di accesso per il proprietario, il gruppo e tutti gli altri
>>- Size: dimensione in byte del file
>>- Timestamps: ctime (cambiamento di un attributo),atime (solo lettura)
>>- Link count: numero di hard links
>>- Data pointers: puntatore alla lista dei blocchi che compongono il file
>
>Questi dati vengono salvati all'interno della *tabella inode* che si trova all'inizio del disco.

## Permessi di accesso ai file

- **Utente proprietario**: solitamente chi crea il file/directory
- **Gruppo proprietario** gruppo primario dell'utente proprietario
Il *proprietario* definisce i permessi di accesso: chi può leggere, scrivere, eseguire un file/directory

slide 40