 >[!example] Raffinamento di travel to the moon
 >1)  Crociera
 >	1.1 Codice (stringa)
 >	1.2 Data di inizio
 >	1.3 Data di fine
 >	1.4 Nave utilizzata (vedi 2)
 >	1.5 itinerario seguito (vedi 4)
 >	1.6 Tipo, uno. tra
 >		1.6.1 luna di miele, di cui interessa
 >			1.6.1.1 sottotipo, uno tra 
 >				1.6.1.1.1 tradizionali: quelle che prevedono un nmero di destinazioni romantiche (v 3.4.1) >= al numero di destinazioni divertenti (v 3.4.2)
 >				1.6.1.1.2 alternative: quelle non tradizionali
 >		1.6.2 per famiglie, di cui interessa
 >			1.6.2.1 se sono adatte per bambini (booleano)
 >
 >2) Nave
 >	2.1 Nome 
 >	2.2 Gradi di comfort (un intero tra 3 e 5)
 >	2.3 Capienza(un intero > 0)
 >3) requisiti sulle destinazioni
 >	3.1 Nome 
 >	3.2 Continente
 >	3.3 Posti da vedere (vedi 5)
 >	3.4 Tipo, uno tra
 >		3.4.1 Romantica
 >		3.4.2 Divertente
 >	3.5 Se è esotica o meno(continente diverso dall'Europa)	
 >4) Itinerari
 >	4.1 Nome
 >	4.2 Sequenza di destinazioni
 >		4.2.1 Destinazione (v. 3)
 >		4.2.2 Arrivo 
 >			4.2.2.1 Ora
 >			4.2.2.2 Numero d'ordine del giorno rispetto alla data di inizio della crociera
 >		4.2.3 ripartenza
 >			4.2.3.1 Ora
 >			4.2.3.2 Numero d'ordine del giorno rispetto alla data di inizio della crociera
 >			
 >	
 >	
 >5) Posti da vedere
 >	5.1 Nome
 >	5.2 orari di apertura (una mappa che associa ad ogni giorno della settimana un insiem di fasce orarie, definita in termini di una coppia di orari
 >6) Clienti
 >	6.1 nome
 >	6.2 cognome
 >	6.3 indirizzo
 >	6.4 età
 >7) Prenotazioni
 >	7.1 crociera (v. 1)
 >	7.2 numero di posti
 >	7.3 istante
 >	7.4 numero di posti prenotati (un intero >0)
 >	7.4 Cliente che effettua la prenotazione
