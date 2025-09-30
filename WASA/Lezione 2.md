# Git pt.2
*Come gestire il conflitto*
- A esegue un fast forward
- B crea un merge commit
- C il merge fallisce e si scatena un conflirro di merge
- D git forza a usare git rebase per mantenere la storia pulita

Ma facciamo un passo indietro.

Git è essenzialmente un file system content addrressable, su questo si costruisce un meccanismo di facciata del versionamento.

Ogni operazione di git commit, nasconde ad un livello più basso una serie di operazioni per creare un oggetto da inserire con un puntatore in una semi-struttura dati.


