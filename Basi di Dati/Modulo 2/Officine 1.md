1 Officina
	1.1 nome
	1.2 indirizzo
	1.3 numero di dipendenti
	1.4 numero di anni di servizio di ogni dipendente
	1.5 dipendente che è il direttore
2 Dipendente
	2.1 nome
	2.2 codice fiscale
	2.3 indirizzo
	2.4 numero di telefono
3 Direttori
	3.1 nome
	3.2 codice fiscale
	3.3 indirizzo
	3.4 numero di telefono
	3.5 data di nascita
4 Riparazione dei veicoli
	4.1 codice
	4.2 veicolo: modello, tipo, targa, anno di immatricolazione, proprietario
	4.3 data e ora di accettazione
	4.4 data e ora di riconsegna (se la riparazione è terminata)
5 Proprietario
	5.1 nome
	5.2 codice fiscale
	5.3 indirizzo 
	5.4 telefono



### Soluzione del prof
1 Requisiti officine
	1.2 nome
	1.3 indirizzo
	1.4 numero di dipendenti
		1.4.1 anni di servizio (intero non negativo)
	1.5 il direttore
2 Requisiti dipendenti
	2.1 nome
	2.2 cognome
	2.3 codice fiscale
	2.4 indirizzo
	2.5 numero di telefono
3 requisiti direttori
	3.1 nome
	3.2 cognome
	3.3 codice fiscale
	3.4 indirizzo
	3.5 numero di telefono
	3.6 data di nascita
	3.7 le officine che dirige (almeno una)
4 requisiti riparazioni
	4.1 codice (stringa univoca)
	4.2 veicolo
	4.3 istante di accettazione
	4.4 se è terminata
		4.4.1 istante di riconsegna
			4.4.1.1 successivo all'istante di accettazione
5 veicoli
	5.1 modello
	5.2 targa (stringa univoca)
	5.3 anno di immatricolazione
	5.4 il proprietario
6 requisiti sui modelli di veicolo
	6.1 nome
	6.2 il tipo
	6.3 la marca
7 requisiti marche di veicoli
	7.1 nome (una stringa univoca)
