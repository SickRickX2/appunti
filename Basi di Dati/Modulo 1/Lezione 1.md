Programma: 
- Algebra relazionale
- Progettazione di una base di dati: Terza Forma Normale (3NF)
- Organizzazione fisica dei dati
- Controllo della concorrenza
## Sistema Informativo
Non necessariamente digitalizzato. Componente di una organizzazione che viene utilizzata per gestire le informazioni di interesse. Costituito da:
- **file** : organizzazione sequenziale
- **applicazione**: scritta in un linguaggio orientato alla gestione di file (Cobol, PL/1)
- **gestione dei dati**: file system
Grazie ai database moderni si sono superati vari problemi come:
- **ridondanza**: se due applicazioni usavano gli stessi dati, venivano replicati
- **inconsistenza**: l'aggiornamento di un dato riguardava una sola copia del dato
- **dipendenza dei dati**: ogni applicazione organizzava i dati tenendo conto dell’uso che doveva farne
- **garantire la privacy** di alcune informazioni specifiche, creando delle liste esterne a seconda delle informazioni necessarie
Una base di dati (database)  è un insieme di file mutuamente connessi. Questi insiemi di dati possono essere organizzati in diverse strutture di dati.
I **database management system DBMS** si servono delle funzioni di basso livello dei sistemi operativi per gestire le tabelle (o file). Sono strumenti software per la gestione di grandi masse di dati residenti su memoria secondaria. Di solito dobbiamo unire più informazioni derivate da tabelle diverse.
Possiamo avere:

- **dati strutturati**: gli oggetti sono rappresentati da brevi stringhe e da numeri
- **dati non strutturati**: testi scritti in un linguaggio naturale

**Relazione** := è un termine ambiguo usato sia in senso matematico che per esprimere una tabella

**Tabella** := rappresentata da uno schema, con degli attributi e una tupla di relazioni.

La struttura dell’informazione dipende da come viene utilizzata e può essere modificata nel tempo.

L' obiettivo di una base di dati è quello di facilitare il recupero di informazioni inserite nelle nostre tabelle (che devono soddisfare certe condizioni).

**Dati** := fatti grezzi che devono essere interpretati e contestualizzati

**modelli logici**: indipendenti dalle strutture fisiche (noi usiamo il **modello relazionale**)

**modelli concettuali**: indipendenti dalle modalità di realizzazione (usato per le prime fasi)

Il modello relazionale ha implementato il riferimento ai dati per valore. (IBM primi anni 70)

Nel MR abbiamo:

- **Oggetto** = _record_
- **Campi** = _Informazioni di interesse_

Lo **Schema della Relazione** è l’insieme degli attributi che caratterizzano le informazioni di interesse dell’oggetto (i nomi degli attributi devono essere significativi già di per sé)
Le tuple costituiscono un’istanza (tabella).
Tabella = Insieme di record di tipo omogeneo.
L’ordine al momento dell'interrogazione non importa, al momento di inserimento invece sì.
Ci sono tre livelli di astrazione di un DB:
![[Pasted image 20240925234114.png|600]]
- **Schema esterno**: descrizione di una porzione della base di dati in un modello logico attraverso "viste parziali" che possono prevedere organizzazioni dei dati diverse rispetto a quelle utilizzate nello schema logico, riflettono esigenze e privilegi di accesso di particolari tipologie di utenti garantendo vari livelli di privacy. Ad uno schema logico si possono associare più schemi esterni.
- **Schema logico**: descrizione dell'intera base di dati nel modello logico "principale" del DBMS, ad esempio la struttura delle tabelle
- **Schema fisico**: rappresentazione dello schema logico per mezzo di strutture fisiche di memorizzazione, cioè i file

Gli accessi alla base di dati avvengono solamente attraverso lo **schema esterno** che può anche coincidere con l'intero schema logico

Due relazioni distinte vengono combinate solo in fase di output non sul disco fisico. Le viste possono essere usate per garantire la privacy, facendo accedere alcuni utenti ad alcune informazioni specifiche lasciando invariata però la memoria fisica.
Bisogna notare che lo **schema** è invariato nel tempo (aspetto **intensionale**) mentre l’**istanza**, i valori attuali invece possono cambiare (aspetto **estensionale**)

I dati devono soddisfare dei “**vincoli**” di dominio che esistono nelle realtà di interesse.( ci sono vari tipi di vincoli)
- dipendenze funzionali
- vincoli di chiave
- vincoli di dominio
- vincolo operativo (non è un vero e proprio vincolo ma per ora lo metto qui)
- vincoli dinamici
Importantissimo proteggere i dati da malfunzionamenti dell'hardware , del software, dall'accesso concorrente alla base di dati e da accessi non autorizzati.

Ricapitolando
I Compiti del DBA
 **Progettazione**
definizione e descrizione di
- chema logico
- schema fisico
- sottoschemi e/o viste
(Data Definition Language)

 **Mantenimento**
- modifiche per nuove esigenze o per motivi di efficienza
- routine: caricamento, copia e ripristino, riorganizzazione, statistiche, analisi)
- prova macbook



