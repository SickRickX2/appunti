Le *grammatiche context free* sono un metodo più potente di per descrivere linguaggi, poiché riescono a descrivere alcuni aspetti che hanno una struttura ricorsiva.
I linguaggi associati alle grammatiche context-free sono chiamati *linguaggi context free*. La classe dei linguaggi context-free include tutti i linguaggi regolari e molti ulteriori linguaggi.

>[!example] Example: 
>Sia $G_{1}$ grammatica context free impostata nel seguente modo:
$$\begin{align} A &\to 0A1 \\ A &\to B \\ B &\to \# \end{align} $$

Una grammatica consiste di un insieme di **regole di sostituzione** anche chiamate *produzioni*. Ogni regola appare come una linea nella grammatica, costituita da un simbolo e una stringa separati da una freccia. Il ismbolo è chiamato *variabile*. La stringa consiste di variabili e altri simboli chiamati *terminali* (numeri, simboli speciali ad es: \#)
La *variabile iniziale* si trova sul lato sinistro della regola più in alto.

Una grammatica può essere usata per descrivere un linguaggio generando ogni stringa del linguaggio nel seguente modo:
 1) Scrivi la variabile iniziale
 2) Sostituisci la variabile scritta con il lato destro della regola in cui compare a sinistra
 3) Ripeti il passo 2 finché non ci sono più variabili

Per esempio, la grammatica $G_{1}$ genera la stringa $000\#111$
Una sequenza di sostituzioni per ottenere una stringa è chiamata una *derivazione*. Una derivazione di questa stringa in $G_{1}$ è:
$A \implies 0A1 \implies 000A111 \implies 000B111 \implies 000\#111$










