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


>[!tip] ### Long term scheduling
>Decide quali programmi sono ammessi nel sistema per esser eseguiti, spesso il criterio adottato è quello FIFO (first in first out). Controlla il grado di multiprogrammazione, più processi ci sono e più è piccola la percentuale di tempo per cui ogni processo viene eseguito
>Strategie tipiche:
>- i lavori batch vengono accodati e il LTS li prende man mano che lo ritiene "giusto"
>- i lavori interattivi vengono ammessi fino a "saturazione" del sistema
>- cerca di mantenere un mix di processi I/O bound e CPU-bound
>- cerca di bilanciare le richieste per i dispositivi I/O
>
>Può essere chiamato in causa anche quando non ci sono nuovi processi, quando termina un processo oppure quando alcuni processi sono idle da troppo tempo

>[!tip] ### Medium Term scheduling
>Fa parte della funzione di swapping dei processi, ovvero del passaggio da memoria secondaria a principale e viceversa, questo passaggio di memorie serve per gestire il grado di multiprogrammazione

>[!tip] ### Short Term scheduling
>Chiamato anche *dispatcher* è quello eseguito più frequentemente, invocato sulla base di eventi come:
>- interruzioni
>- chiamate di sistema
>- segnali
>Il suo scopo è quello di allocare tempo di esecuzione su un processore per ottimizzare il comportamento dell'intero sistema, dipendentemente da determinati indici prestazionali

Ci sono diversi criteri per lo Short Term scheduling, e bisogna distinguere tra criteri per l'utente e criteri per il sistema
- per l'utente: tempo di risposta
- per il sistema: uso efficiente ed effettivo del processore
Inoltre c'è una distinzione tra criteri correlati e non correlati alle prestazioni:
- correlati: tempo di risposta, throughput
- non correlati: predicibilità, equità
#### Criteri Utente
Prestazionali: 
- **Turnaround time** (tempo di ritorno)
- **Response time** (tempo di risposta)
- **Deadline** (scadenza)
Non prestazionali:
- **Predictability** (predicibilità)

#### Criteri di Sistema
Prestazionali:
- **Throughput** (volume di lavoro nel tempo)
- **Processor utilization** (uso del processore)
Non prestazionali
- **Fairness** (equità)
- **Enforcing priorities** (gestione delle priorità)
- **Balancing resources** (bilanciamento nell'uso delle risorse)

La modalità di decisione specifica in quali istanti di tempo la funzione di selezione viene invocata, 

