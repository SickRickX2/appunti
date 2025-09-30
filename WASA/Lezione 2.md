# Git pt.2
*Come gestire il conflitto*
- A esegue un fast forward
- B crea un merge commit
- C il merge fallisce e si scatena un conflirro di merge
- D git forza a usare git rebase per mantenere la storia pulita

Ma facciamo un passo indietro.

Git è essenzialmente un file system content addrressable, su questo si costruisce un meccanismo di facciata del versionamento.

Ogni operazione di git commit, nasconde ad un livello più basso una serie di operazioni per creare un oggetto da inserire con un puntatore in una semi-struttura dati.

Usiamo una struttra ad albero per comodità. All'interno ci sono blob (nodi) o altri tree (praticamente altre cartelle). Questo albero viene manipolato tramite i nostri commit e le operazioni effettuate tramite git.

Possiamo forzare la creazione di un indice su un determinato oggetto.

- *checkout*: sposta la cwd alla branch specifica
- *cherrypick*: è una sorta di rebase ma non sull'ultima versione, quindi non aggiunge ma sovrascrive

>[!note]
>- **Main** sono codice stabile, testato e rilasciato. Merge in: solo da realese
>- **Develop**: cronologia completa delle funzionalità di sviluppo. Merge da: features
>- **Feature**: Lavoro isolato su una nuova funzionalità. Ramifica da develop e unisce in develop
>- **Release**: preparazione e rifinitura finale per il prossimo rilascio
>- **Hotfix**: piccoli cicli di sviluppo che servono per la correzione retroattiva e propagano verso main e verso develop

## Remote
Riferimenti ai branch in repository remoti. **Origin** è il nome remoto predefinito.
Il tracking viene eseguito tramite branch locali con relazione diretta a un remoto.
Git pull e git push fanno implicitamente tracking.
*Se avviene una divergenza storica?*
Se una linea di sviluppo diverge e abbiamo bisogno di riconciliare, utilizziamo un merge.
git pull -> è l'unione di git fetch seguito da git merge
Scarica il contenuto da remoto e lo unisce immediatamente nel branch locale corrente
git push -> carica le modifiche verso il remote



