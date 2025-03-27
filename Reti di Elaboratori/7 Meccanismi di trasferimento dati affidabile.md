>[!note] Stop and wait
>Realizziamo una connessione con controllo di flusso e controllo degli errori
>Il mittente e destinatario possono operare solo so un pacchetto alla volta. Una volta che il pacchetto arriva al destinatario viene fatto il checksum e 
>- viene mandato l'ack al mittente
>- oppure viene scartato senza informare il mittente
>
>Il mittente deve tenere una copia del pacchetto finché non riceve riscontro