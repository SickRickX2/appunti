Le strutture dati servono a memorizzare e a organizzare i dati in memoria in modo da poterli utilizzare efficientemente. In Java le principali strutture dati sono implementate attraverso una serie di interfacce che formano il Java Collection Framework.

Le collection si basano su una gerarchia di interfacce dove l'interfaccia *collection<E.>* ne è la radice.

*Collection* è l'interfaccia madre di tutte le collezioni in Java e questa estende l'interfaccia *Iterable* per permettere di iterare su gli elementi di una collezione.

Ci sono tre principali interfacce:
- *List<E.>*: collezioni ordinate che possono contenere duplicati
- *Set<E.>*: collezioni non ordinate che non contengono duplicati
- *Queue*<E.>: collezioni basate sulla struttura FIFO

>[!note]  Mappe
>Le mappe sono strutture dati basate sull'associazioni chiave-valore e sono implementate attraverso l'interfaccia Map, la quale, nonostante non estenda Collection, fa comunque parte del Java Collection Framework


## Lists
Le liste sono strutture dati che implementano l'interfaccia List e memorizzano i dati in modo sequenziale e dinamico. Ciò significa che le liste possono aumentare o diminuire la loro dimensione in base alle esigenze.

Le lsite più utilizzate sono ArrayList e LinkedList
>[!note] Arraylist
>L'Arraylist è una struttura dati ad accesso casuale che permette di accedere direttamente ad ogni elemento della lista. E' implementata attraverso un array a cui è stata aggiunta una funzionalità di ridimensionamento automatico.
>Caratteristiche:
>- **Accesso casuale**, è possibile accedere direttamente a ogni elementio della lista
>- **Ridimensionamento automatico**

>[!note] LinkedList
>In una LinkedList, ogni elemento è rahppresentato da un nodo che contiene un valore e un riferimento al nodo successivo.
>Caratteristiche:
>- **Accesso sequenziale**
>- **Inserimento e rimozione** senza dover riallocare tutta la struttura dati
>- **Accesso Lento**, bisogna scorrere tutti gli elementi per accederne ad uno specifco
>- **Memoria aggiuntiva** per memorizzare anche i puntatori ai nodi


## Set
I set sono collezioni prive di duplicati che estendono la classe AbstractSet ed implementano l'interfaccia Set. Gli oggetti inseriti nei set devono implementare correttamente i metodi hashCode ed equals.

Esistono tre tipi di set:
- HashSet
- TreeSet
- LinkedHashSet

>[!note] HashSet
>Gli elementi della collezione vengono memorizzati in una tabella di hash, questi implica costi di ricerfa ed inserimento veloci e l'assenza di un ordinamento

>[!note] TreeSet
>Memorizza gli elementi della collezione in una struttura ad albero mantenendo il  loro ordine naturale trammite *compareTo()*. Questa struttura ci permette di cercare, rimuovere e inserire elementi con costo log(n)

>[!note] LinkedHashSet
>Memorizza gli elementi in una tabella hash proiprio come un HashSet ma allo stesso tempo mantiene una copia dei dati in una struttura simile ad una LinkedList. Questo permette di avere le prestazioni di un set ma l'ordinamento e inserimento di uan LinkedList. Ovviamente comporta ad un maggiore uso della memoria per le due strutture dati.


## Maps
Sono strutture dati che implementano l'interfaccia Map ed organizzano i dati in coppie chiave-valore, in cui non possono esistere due elementi con la stessa chiave.
Di base non è possibile iterare sulle mappe ma è possibile ottenere il set delle chiavi o il set dei valori su cui è possibile iterare.

Ci sono tre tipologie di mappe:
- HashMap
- TreeMap
- LinkedHashMap

>[!note] HashMap
>Memorizza la coppia chiave-valore in una tabella hash

>[!note] TreeMap
>Memorizza le coppie chiave-valore in una struttura ad albero che mantiene l'ordinamento naturale

>[!note] LinkedHashMap
>Memorizza le coppie chaive-valore in una tabella hash proprio come un HashMap ma allo stesso tempo mantiene una copia dei dati in una struttura dati in una struttura simile ad una LinkedList

