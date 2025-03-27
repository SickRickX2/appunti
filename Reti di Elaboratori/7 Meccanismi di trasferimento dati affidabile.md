>[!note] Stop and wait
>Realizziamo una connessione con controllo di flusso e controllo degli errori
>Il mittente e destinatario possono operare solo so un pacchetto alla volta. Una volta che il pacchetto arriva al destinatario viene fatto il checksum e 
>- viene mandato l'ack al mittente
>- oppure viene scartato senza informare il mittente
>
>Il mittente deve tenere una copia del pacchetto finché non riceve riscontro. La finestra di invio serve per tenere traccia del pacchetto.
>
>>[!tip] Numeri di sequenza e riscontro nello stop e wait
>>Per gestire i pacchetti duplicati viene verificato l'intervallo più piccolo della comunicazione senza ambiguità.
>>Se si invia un pacchetto con numero di sequenza x, si possono verificare 3 casi:
>>- Il pacchetto arriva correttamente al destinatario che invia un riscontro con pacchetto successivo = x+1
>>- Il pacchetto risulta corrotto o non arriva al destinatario, viene nuovamente inviato il pacchetto x
>>- Il pacchetto arriva correttamente ma il discorso viene perso o corrotto. Scade il timer e il mittente rispedisce pacchetto x. Si crea un duplicato.
>
>>[!example] FSM mittente
>
>
>>[!danger] Problema di efficienza
>>Se il rate è alto ma il ritardo è consistente lo stop and wait è inefficiente. Funziona ma non permette di usare la rete al meglio

# Meccanismi con pipeline
Sono meccanismi che non inviano pacchetti uno ad uno ma continuano ad inviarne prima di ricevere tutti gli ack.
>[!note] Go back n
>Abbiamo una finestra di invio di più posizioni e una di ricezione da una sola posizione.
>Devo tenere traccia dell'invio nella finestra mittente. Abbiamo quindi due puntatori, uno per gli ack dei pacchetti inviati e uno per il prossimo pacchetto da spedire.
>Rispetto allo stop and wait l'ack indica ancora il numero di sequenza del prossimo pacchetto atteso ma è *cumulativo*, tutti i pacchetti fino al numero di sequenza indicato nell'ack sono stati ricevuti correttamente.
>>[!tip] Timer e rispedizione
>>Abbiamo un timer associato al più vecchio pacchetto spedito non ancora riscontrato. Allo scadere del timer si va indietro fino all'inizio (*Go back N*).
>
>**Relazione tra dimensione di finestra di invio e spazio dei numeri di sequenza**
>Possiamo avere una finestra di dimensione $2^m$?
>No deve essere di dimensioni $2^m-1$ altrimenti si rischiano duplicati.

>[!note]  Ripetizione selettiva
>Il mittente rimanda solo i pacchetti ai quali non ha ricevuto gli ack. 
>Il timer del mittente per ogni pacchetto non riscontrato.
>Non c'è più un *ack comulativo* ma specifici per ogni pacchetto.
>Quando scade un timer si rinvia il pacchetto specifico
>>[!example] FSM

### Protocolli bidirezionali: piggybacking
Abbiamo pacchetti in una direzione e eack in quella opposta, in realtà viaggiano entrambi nelle due direzioni.










