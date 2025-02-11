Le strutture dati servono a memorizzare e a organizzare i dati in memoria in modo da poterli utilizzare efficientemente. In Java le principali strutture dati sono implementate attraverso una serie di interfacce che formano il Java Collection Framework.

Le collection si basano su una gerarchia di interfacce dove l'interfaccia *collection<E.>* ne è la radice.

*Collection* è l'interfaccia madre di tutte le collezioni in Java e questa estende l'interfaccia *Iterable* per permettere di iterare su gli elementi di una collezione.

Ci sono tre principali interfacce:
- *List<E.>*: collezioni ordinate che possono contenere duplicati
- *Set<E.>*: collezioni non ordinate che non contengono duplicati
- *Queue*<E.>: collezioni basate sulla struttura FIFO

>[!note]  Mappe
>Le mappe sono strutture dati basate sull'associazioni chiave-valore e sono implementate attraverso l'interfaccia Map, la quale, nonostante non estenda Collection, fa comunque parte del Jaca 
