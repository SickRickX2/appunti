Gestisce le risorse hardware di un sistema computerizzato (processori, RAM, IO) e fornisce un unsiem di servizi agli utenti.
1) **Processore** si occupa delle computazioni
2) **Memoria principale** è volatile, se il PC si spegne se ne perde il contenuto (chiamata reale o primaria)
3) **IO** memoria secondaria non volatile (dischi), comunicazione (scheda di rete), tastiera ecc...
4) **Registri**
	1) *visibili dall'utente* usati dai linguaggi non interpretati
	2) *di controllo e di stato* usati dal processore per controllare il suo utilizzo, e dal sistema operativo per controllare l'esecuzione dei programmi
	3) *Interni*: usati dal processore, responsabili della comunicazione con memoria e IO
##### Registri visibili all'utente
Sono gli unici che posssono essere usati direttamente quando si prpogramma in un linguaggio macchina. Possono contenere dati o indirizzi (puntatori)
#### Registri interni
I principali registri interni sono:
- *registro di indirizzo di memoria (MAR)* contiene l'indirizzo della prossima operazione di lettura/scrittura
- *registro di memoria temporanea(Memory Buffer Register)* contiene i dati da scrivere in memoria, o lo spazio dove scrivere i dati letti dalla memoria
- *IO address register*
- *IO buffer register* registro di memoria temporanea per IO
#### Registri di controllo e stato
- *Program counter* contiene l'indirizzo dell'istruzione da prelevare dalla memoria
- *Instruction Register* contiene la più recente istruzione prelevata
- *Program Status Word* contiene le informazioni di stato
- *Flag* singoli bit settati dal processore come risultato di operazioni
#### Esecuzione di istruzioni
Due passi:
- fase di *fetch* delle istruzioni: il processore legge il program counter e preleva dalla memoria principale le istruzioni
- fase di *execute* il processore esegue le istruzioni prelevate

## Interruzioni
le interruzioni interrompono la normale esecuzione sequnziale del processo --> come conseguenza viene eseguito software di sistema, parte del sistema operativo.
Le cause sono molteplici, e danno 
