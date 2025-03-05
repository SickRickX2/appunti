>[!note] Vincoli di identificazione
>Mettendo un *id* diciamo che non possono esistere due oggetti con lo stesso attributo (id) uguale. Si può anche mettere un id definito su più attributi

## Ereditarietà
In UML permette di implementare il concetto di ''sottoclasse''. Viene chiamata *relazione is-a*, ogni sottoclasse è anche un'istanza della propria superclasse. 
>[!note] Classi più specifiche di un oggetto
>Una classe, a differenza dei linguaggi di programmazione, può espendere anche più di una classe. ![[Pasted image 20250305153022.png]] 
>L'insieme delle classi più specifiche di 'anna' è {Studente, Lavoratore} ma non Persona anche se 'anna' è istanza di Persona, Studente, Lavoratore

>[!example] Azienda 1
>1) Impiegato
>	1.1 nome: Stringa
>	1.2 cognome: Stringa
>	1.3 data di nascita: Data
>	1.4 stipendio: reale >= 0
>	1.5 dipartimento di afferenza (uno)  (vedi 2)
>		1.5.1 data di afferenza
>	1.6 Progetti (anche nessuno)
>2) Dipartimento
>	2.1 nome: Stringa,univoca
>	2.2 telefono: intero
>	2.4 Direttore (è un impiegato vedi 1)
>3) Progetto
>	3.1 nome (stringa)
>	3.2 budget (un reale >=0)
>	3.3 Immpiegati partecipanti (v.1)


