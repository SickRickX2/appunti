## Diagramma delle classi e degli oggetti per l'analisi
Nella fase di analisi si concentra più delle classi che sugli oggetti. 

>[!note] Oggetto
>Un oggetto in UML modella un elemento del dominio di analisi che:
>- ha vita propria
>- è istanza di una classe
>- è identificato univocamente mediante l'identificatore di oggetto

>[!note] Classi
>Una classe modella un insiem di oggetti omogenei ai quali sono associate proprietà statiche e dinamiche.
>Ogni classe è descritta da:
>- un nome
>- un insieme di proprietà

>[!note] Associazioni
>Un'associazione modella la possibilità che oggetti di due o più classi abbiano dei legami. Devono avere un nome e possono avere una direzione di lettura opzionale

>[!note] Link
>I link sono istanze delle associazioni, a contrario degli oggetti però i link non hanno identificatori esplicit: un link è implicitamente identificato dalla coppia. Questo indica che la coppia o esiste o non esiste, non ci sono ripetizioni di link (come nell'insiemistica)

>[!tip] Vincoli e molteplicità
>UML permette di definire vincoli di integrità in un diagramma delle classi. Un vincolo di integrità impone ulteriori restrizioni sui livelli estensionali ammessi. 

>[!warning] Vincolo di molteplicità
>La sinossi per mettere questo vincolo è la seguente
>![[Pasted image 20250304150930.png]]

>[!danger] Associazioni che insistono più volte sulla stessa classe
UML quando abbiamo un'associazione che insiste più volte sulla stessa classe ci obbliga a dare esplicitamente nomi distinti ai due ruoli ![[Pasted image 20250304153136.png]]

>[!note] Associazioni con attributi (Association class)
>In UML si può definire un'associazione con attributi, sembra una classe ma il nome inizia con la lettera minuscola ed è legata con una linea tratteggiata all'associazione. Si comporta come una classe perché può essere a sua volta terminale di ulteriori associazioni.
>>[!danger] Attenzione
>>Anche in presenza di attributi, la natura dell'associazione non cambia, non si può avere più di un link con la stessa coppia di oggetti

## Tipi di dato concettuali
>[!note] Tipi Base
>Vogliamo utilizzare tipi concettuali che siano facilmente realizzabili con qualsiasi linguaggio o tecnologia:
>- Intero
>- Stringa
>- Reale
>- Booleano
>- Data
>- Ora
>- DataOra

Vogliamo però anche modellare la realtà in modo accurato
>[!note] Tipi specializzati
>UML permette di definire tipi di dato specializzati.

>[!note] Tipi enumerativi
>Quando i valori di un attributi sono pochi, finiti, immutabili...allora possiamo usare un insieme enumerativo. Bisogna solo usarli quando siamo ragionevolmente sicuri che i valori non cambiano. Elenca valori che non sono stringhe ma *etichette*

## Tipi di dato composto
UML consente di definire anche tipi di dato composti da più campi: *tipi record*.


