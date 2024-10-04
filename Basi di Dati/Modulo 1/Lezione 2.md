#  Il Modello Relazionale
>[!note] Il **modello relazionale** è basato sul concetto matematico di relazione (nel nostro caso le tabelle). I dati e le relazioni(riferimenti) vengono rappresentati come valori.

>[!warning] Relazione ha diversi significati:
> - Relazione matematica: come nella teoria degli insiemi
>- Relazione secondo il modello relazionale di dati quindi insiemi caratterizzati ognuno dai propri campi
> - Relazione (dalll'inglese relationship) che rappresenta una classe di fatti, nel modello concettuale entità-relazioni.

Il modello relazionale si basa su un *dominio* (un insieme infinito di valori). Ci sono **domini di base** e **domini costruiti** dai domini di base. In questo modello i campi vanno valorizzati in base ai vincoli, formando una *tupla*, che a loro volta formano un'*istanza* di una relazione. 

>[!tips] Una relazione matematica è un qualsiasi sottoinsieme del prodotto cartesiano di uno o più *domini*. Una relazione di k domini si dice che è di grado k. La cardinalità di una relazione è data dal numero di tuple che la compongono. **Non c'è in nessun caso** un ordinamento delle tuple. Poiché una relazione è un insieme di tuple non ci possono essere duplicati (non compariranno mai due tuple uguali).

>[!note]  
>*Grado relazione* = **numero domini**
*Cardinalità relazione* = **numero tuple**

Quasi sempre usiamo i domini **predefiniti(o domini base)**: stringhe, interi, reali. Bisogna sempre ricordare che da soli gli attributi non ci dicono nulla, il significato dell'istanza infatti ce lo dà lo **schema relazionale**.

Un **attributo** è definito dal nome e dal dominio dell'attributo. Una relazione può essere implementata come una tabella in cui ogni riga è una tupla della relazione e ogni colonna corrisponde ad una colonna, mentre la coppia attributo-dominio possiamo chiamarlo attributo, un insieme di attributi è uno schema. 

Lo **schema** di una base di dati è un insieme di relazioni con nomi differenti. Lo schema di base di dati relazionale è un insieme di schemi di relazione. 
>[!example]  Funzionamento
>Tabella master -> esporta un valore univoco nella -> tabella slave (riferimento per valore).


Ogni campo di una tabella(che non sia un campo chiave) può contenere un valore *null*(può significare mancanza di informazione o il fatto che l'informazione non è applicabile).
Una *chiave* di una relazione è un **attributo** o **insieme di attributi** che identifica univocamente una tupla. Un insieme che contiene una chiave, si dice **superchiave** (una chiave è anche superchiave perché contiene se stessa ma non è detto che sia vero il contrario).
Una relazione potrebbe avere più chiavi alternative. Si sceglie quella più usata o quella composta da un numero minore di attributi = chiave *primaria*. La chiave primaria **non ammette valori nulli**.
*Vincolo di integrità referenziale*(**foreign key**) ci permette di distinguere le tuple all'interno di una relazione. I vincoli si impostano sulle coppie e non sui singoli attributi. Non tutte le proprietà di interesse possono essere rappresentate tramite vincoli espliciti nel modello logico. le dipendenze funzionali vengono definite direttamente nello schema prima ancora di inserire i dati, così da aggiungere una tupla solo se soddisfa tutti i vincoli imposti  *istanza legale*.
Una dipendenza funzionale stabilisce un particolare legame semantico tra due insiemi non vuoti di attributi X,Y appartenenti ad uno schema R. Tale vincolo si scrive: *X->Y* e si legge **X determina Y**. Una convenzione importante da usare: quando usiamo le **prime lettere** dell'alfabeto intendiamo i **singoli elementi** degli attributi, quando usiamo le **ultime** intendiamo **insiemi di attributi** (*attenzione che un insieme può anche essere un singolo attributo ma non viceversa*).
Diremo che una relazione r con schema R soddisfa la dipendenza funzionale  
X -> Y se
- la dipendenza funzionale è applicabile ad R
- le ennuple di r che concordano su X concordano anche su Y, cioè per ogni coppia di ennupla t1,t2 in r
	 t1[X] = t2[X] -> t1[Y] = t2[Y].
se sono uguali su X devono essere uguali anche su Y.
Se una dipendenza ha come determinante una chiave o una superchiave, la dipendenza non può essere violata.

# Algebra Relazionale
E' un linguaggio formale che ci permette di interrogare le istanze (estrarre le informazioni che ci interessano). Consiste in un insieme di operatori che ci permettono in maniera procedurale, costruendo passo passo l'interrogazione, di arrivare alla soluzione. Gli operatori possono essere binari o unari, i risultati possono essere salvati in una nuova istanza di relazione.
**Proiezione**
Si definisce col simbolo del *$\pi$*, il pedice sono gli attributi dello schema su cui vogliamo proiettare gli attributi della nostra istanza, seleziona le colonne di r che corrispondono agli attributi della istanza.
**Selezione**
Si definisce col simbolo $\theta$ e ci consente di effettuare un taglio orizzontale su una relazione, cioè di selezionare solo le righe/tuple che soddisfano una data condizione. la condizione di selezione è un espressione booleana composta, in cui i termini semplici sono del tipo:
- A$\theta$B
- oppure
- A$\theta$'a'
dove:
theta è un operatore di confronto.



