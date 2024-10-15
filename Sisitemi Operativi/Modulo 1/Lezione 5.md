>[!note]  ## Scheduling
>Lo *scheduling* (tradotto: pianificazione) serve al processore per allocare le risorse tra diversi processi che ne fanno richiesta contemporaneamente. Per raggiungere questo obiettivo vanno ottimizzati vari aspetti:
>- tempo di risposta
>- throughput
>- efficienza del processore
>
Lo scheduling ha vari obiettivi tra cui: 
>- distribuire il tempo di esecuzione in modo *equo* tra i vari processi
>- gestire le priorità dei processi
>- evitare la *starvation* dei processi
>- usare il processore in modo efficiente
>- avere un overhead basso

Ci sono vari tipi di scheduling:
**Long-term scheduling**: decide l'aggiunta ai processi da essere eseguiti
**Medium-term scheduling**: decide quale processo, tra quelli pronti, va eseguito da un processore
**I/O scheduling**: decide a quale processo, tra quelli con una richiesta pendente per l'I/O, va assegnato il corrispondente dispositivo I/O


>[!tips###