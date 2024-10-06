>[!note] Livelli:
>1) Ci sono alcuni compiti delegati all'hardware e alcuni delegati al SO
>2) insiemi di istruzioni macchina
>3) operazioni di chiamata e ritorno e subroutine
>4) interruzioni
>5) *processo* come programma in esecuzione
>6) dispositivi di memorizzazione secondaria, trasferimento di blocchi di dati 
>7) gestione dello spazio logico degli indirizzi (gestione della memoria)
>8) comunicazioni tra processi
>9) salvataggio di lungo termine di file con nome (filesystem)
>10) accesso ai dispositivi esterni 
>11) associazione tra identificatori interni esterni
>12) supporto di alto livello per i processi
>13) interfaccia utente
# Processo
>[!note] E' un'**istanza di un programma** in esecuzione, il SO deve permettere che la stessa applicazione possa essere avviata/istanziata più volte in maniera indipendente l'una dall'altra. Il processo è caratterizzato da una **sequenza di istruzioni**, uno **stato corrente** (tutte le risorse che il processo utilizza, stato delle variabili ecc...) e da un insieme associato di **risorse**; è composto da:
>- codice
>- insieme di dati
>- insieme di attributi che descrivono lo stato del processo

*Processo in esecuzione* lo intendiamo come un utente che richiede l'esecuzione di un programma che ancora non è terminato. Questo significa che il processo è in esecuzione sul processore, dietro ogni processo c'è un programma.

Il Ciclo di vita del processo ha 3 macrofasi: *creazione, esecuzione, terminazione*.

>[!example] .
> Nella fase di creazione il SO deve accettare la richiesta di creazione del processo e va ad impostare tutte le risorse e strutture dati per l'esecuzione del processo(una fase di setup), in seguito abbiamo l'esecuzione. La terminazione può essere prevista oppure non prevista. 


Finché il processo è in esecuzione abbiamo bisogno di generargli un **identificatore** e di **osservare il suo stato**. Inoltre dobbiamo tener conto della priorità dei vari processi (ci sono processi più importanti di altri), fondamentale anche *l'hardware context* che contiene informazioni relative al valore corrente dei registri della CPU (vedremo più avanti perché è importante salvare il contesto di esecuzione del processo) che include il **program counter**, bisogna considerare che il contesto viene aggiornato solo in casi particolari. Abbiamo bisogno anche di puntatori alla memoria che definiscono l'*immagine della memoria*, informazioni sullo stato di I/O e le informazioni di **accounting** (quale utente lo segue) fondamentale per la privacy e la sicurezza.

>[!tip]  Process Control Block
Tutte queste informazioni vengono contenute nel **Process Control Block**, contiene gli elementi del processo e ce n'è uno diverso per ogni processo. Permette al SO di gestire più processi contemporaneamente, contiente le informazioni necessarie per l'esecuzione,l'arresto e la sospensione.
La **traccia (trace)** di un processo è la sequenza di istruzioni eseguita dal processo. Il **dispatcher** è un componente del SO che si occupa di scambiare i processi in esecuzione, si trova **sempre** in memoria.
Modello di processi a 2 Stati:
>1) In esecuzione
>2) Non in esecuzione (ma è comunque un processo "attivo")
(In realtà è oversemplified in questo modo)

>[!note]
Il **dispatcher** decide come scambiare i processi grazie al sistema *a coda*. Prende i processi dalla coda e lo mette in esecuzione del processore, viene messo in pausa alla fine della coda e si ricomincia.
In un SO ci sono almeno un processo in esecuzione (n>= 1).  I processi possono essere creati dal SO oppure dall'utente tramite l'interfaccia utente. *Process spawning* c'è sempre un processo padre che crea il processo figlio.
C'è sempre un processo *master* che non può essere terminato.

**Modello dei processi a 5 Stati:** *new, ready, running, exit, blocked*
- *new*: crea risorse e strutture dati
- *ready*: il processo è pronto per essere eseguito
- *running*: esecuzione del programma
- *blocked*: processo bloccato finché non arriva un determinato evento che lo sblocca
- *exit*: distrugge le strutture dati e le risorse vengono riallocate
Con questo modello vengono usate due code invece di una (in realtà sono multiple).

>[!warning] 
>Le risorse disponibili sono limitate quindi solo un determinato numero di processi può stare nello stato ready allo stesso momento, più grande è l'image process più processi saranno in esecuzione contemporaneamente. Anche un processo in stato blocked riempie la memoria e potrebbe creare dei problemi.

###### Ha senso che un blocked occupi la ram finché non viene sbloccato da un evento? 
Non è una situazione ottimale, si può ottimare introducendo lo stato **suspended** (sospeso). Questo stato va ad indicare i processi che non sono pronti ad eseguire spostati dallla memoria principale alla memoria secondaria per liberare la memoria della RAM.
Si possono implementare anche due stati suspended (una transizione intermedia tra blocked/suspended e ready/suspended)
Ci sono diversi motivi per sospendere un Processo

|     |     |
| --- | --- |
|     |     |



