## Forwarding datagrammi IP
Inoltrare significa collocare il datagramma sul giusto percorso che lo porterà a destinazione, inviandolo al prossimo hop. L'inoltro richiede una riga nella tabella per ogni blocco di rete.

## Routing
Il routing costruisce e determina il percorso migliore da seguire che poi verrà usato dal forwarding (sempre tramite tabella).

## Routing intra-dominio: RIP
(*intradominio* vuol dire ad esempio all'interno di un ISP, viene fatto routing solo su una parte di rete e non su quella globale) 

>[!tip] Algoritmo Distance Vector
>- *Distribuito*: ogni nodo riceve informazione dai vicini e opera su quelle
>- *Asincrono* non richiede che tutti i nodi operino al passo con gli altri
>
>Si basa su:
>1) Equazione di Bellman-Ford
>2) Concetto di vettore di distanza
>
>**Equazione di Bellman-Ford**:
>Definisce 
>$D_x(y):=$ il costo (o la distanza) del percorso a costo minimo dal nodo x al nodo y
>
>Allora:
>$D_x(y) = min_v\{c(x,v)+D_v(y)\}$
>dove $min_v$ riguarda tutti i vicini di x
>
>**Vettore distanza**
>Un albero a costo minimo è una combinazione di percorsi a costo minimo dalla radice dell'albero verso tutte le destinazioni.
>Il vettore di distanza è un array monodimensionale che rappresenta l'albero. Un vettore di distanza non fornisce il percorso da seguire per giungere alla destinazione ma solo i costi minimi per le destinazioni.
>![[Pasted image 20250430124008.png]]
>
>>[!warning] Come viene creato il vettore distanza?
>>Ogni nodo della rete quando viene inizializzato crea un vettore distanza iniziale con le informazioni che il nodo riesce ad ottenere dai propri vicini (quelli a cui è collegato direttamente). Per creare il vettore dei vicini invia messaggi di *hello* attraverso le sue interfacce (e lo stesso fanno i vicini) e scopre l'identità dei vicini e la sua distanza da ognuno di essi. Il vettore iniziale rappresenta il vettore a costo minimo verso i vicini. Dopo che ogni nodo ha creato il suo vettore ne invia una copia ai suoi vicini.

Ogni volta che un nodo riceve una copia dal vicino confronta le informazioni del proprio vettore con quello in arrivo e sceglie il minimo. 

$D_x(y) \leftarrow min_v\{c(x,v)+D_v(y)\}$

Ogni volta che un nodo aggiorna il proprio vettore distanza invia la copia aggiornata ai vicini.
**Algoritmo**
per tutte le destinazioni y in N:
	if $y$ è un vicino:
		$D_x(y) = c(x,y)$
	else: $D_x(y) = \infty$ 
per ciascun vicino $w$
		invia il vettore distanza $D_x$ = \[$D_x(y)$ :$y$in $N$] a w
### Problema della modifica dei costi
Con questo algoritmo si verifica il problema nel momento in cui c'è un guasto tra dei collegamenti.
**Problema del conteggio infinito**: *le buone notizie viaggiano in fretta, le cattive notizie si propagano lentamente*

 **a. Prima del guasto:**

- A raggiunge X con costo 1.
    
- B pensa di raggiungere X tramite A con costo 2.
    

**b. Guasto del collegamento tra A e X:**

- A perde il collegamento diretto con X.
    
- A non sa più raggiungere X, ma **B non lo sa ancora**.
    

 **c. A si aggiorna da B:**

- A riceve da B la "vecchia" informazione che X si raggiunge con costo 2.
    
- A aggiorna il suo vettore e crede che X sia raggiungibile tramite B con costo 3.
    

 **d. B si aggiorna da A:**

- B riceve da A che X si può raggiungere con costo 3.
    
- B aggiorna il suo vettore e ora pensa di poter raggiungere X con costo 4.
    

 I pacchetti "rimbalzano" tra A e B, aumentando ogni volta il costo.

 **e. Alla fine:**

- Dopo **molti aggiornamenti**, entrambi capiscono che X **non è raggiungibile**.
    
- Il costo diventa "infinito" (o un valore massimo stabilito, tipo 16 nei protocolli RIP).


 >[!note] Split Horizon
 >Invece di inviare la tabella attraverso ogni interfaccia, ciascun nodo invia solo una parte della sua tabella tramite le interfacce. Se ilnodo B ritiene che il percorso ottimale per raggiunger il nodo X passi attraverso A, allora NON deve fornire questa informazione ad A perché dovrebbe già saperlo.
 
 >[!note] Poisoned reverse 
 >Si pone ad $\inf$ il valore del costo del percorso che passa attraverso il vicino a cui si sta inviando il vettore.
 
>[!note] RIP (Routing Information Protocol)
>è un protocollo a vettore distanza, distanza misurata in hop (max= 15, infinito = 16)
>


>[!tip] Messaggi RIP
>RIP si basa su una coppia di processi client-server e sul loro scambio di messaggi.
>-*RIP request*: quando un nuovo router viene inserito nella rete invia una RIP Request per ricevere immediatamente informazioni di routing
>- *RIP Response*: in risposta ad una request o periiodicamente ogni 30 sec
>
>**Struttura dei messaggi**
>

### Timer RIP 
- **Timer periodico**: ogni 25-35 secondi controlla l'invioi di messaggi di aggiornamento
- **Timer di scadenza**: regola validità dei percorsi, se entro lo scadere del timer non si riceve aggiornamento, il percorso viene considerato scaduto e il suo costo impostato a 16
- **Timer per garbage collection**: elimina percorsi dalla tabella, quando le informazioni non sono più valide il router continua ad annunciare il percorso con costo pari a 16 e allo scadere del timer rimuove il percorso.
