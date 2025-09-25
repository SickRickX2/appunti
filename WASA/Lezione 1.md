Progetto: simulazione di whatsapp; utenti si scambiano messaggi testuali o di immagini.

## Git
Motivi per cui utilizziamo git:
- Bisogna usare delle convenzioni per i nomi
- Bisogna avere uno storico dei cambiamenti
- Bisogna avere informazioni dell'autore
- Evitare duplicazione del contenuto

**TERMINI CHIAVI**
- *repository*: set di commit, branch e tag; assumiamo 1 progetto = 1 repo
- *working copy/directory*: una cartella del file system del progetto con i file tracciati dal sistema di revisionamento
- *commit*: il codice in un punto del tempo
- *branch*:una linea di sviluppo, è un insieme ordinato di commit
- *merge*:l'azione di fondere due o più branch
- *tag*:un etichetta personalizzata allegata ad un commit
- *fork*:un nuovo repository che è una copia di uno esistente
- *pull/merge request*:una richiesta di unire il codice da un fork o branch al repository/branch padre
- *SHA1* algoritmo usato per l'hashing di git
- campi obbligatori di un commit:
	- data+autore,data+committer
	- commento **obbligatorio** spiegare il commit, cosa è cambiato ecc...
	- 0,1 o più genitori
	- tree:hash di tutti i (~) file nel commit
### Staging
Il commit può contenere un sottinsieme delle modifiche, è necessario aggiungere alla staging area i cambiamenti. 
Dobbiamo esplicitamente specificare i file da includere nel commit.

>[!note] Branch
>Punta sempre all'ultimo commit e inizia dall'ultimo commit orfano (di solito primo commit del repo). Il primo commit quindi crea il primo branch, permette di lavorare in parallelo a più versioni

>[!tip] Head
>Posizione corrente nella storia -> working copy.
>Può putare ad un commit specifico, ad un branch o ad un tag.
>*Checkout* è la primitiva corrispondente (aggiorna la working copy)
>>[!warning] Se non si punta ad un branch, detached head -> no commit

### Operazioni
>[!note] Merge
>Ci sono tre strategie:
>- **fast forward**: il merge è valido se un branch è continuazione diretta dell'altro
>- **merge commit**:
>- **rebase**:

