Si occupa del trasferimento dei datagrammi nel momento incui abbiamo un host mittente e un host destinatario.
Funzioni chiave:
- *Inatradamento (routing)*: determina il percorso seguito dai pacchetti dall'origine alla destinazione (la strada che deve fare il pacchetto per arrivare a destinazione).
- *Inoltro(forwarding)*: trasferisce i paccchetti dall'input del router all'output del router appropriato.

Ogni router ha la propria tabella di routing.

### Switch e Router
Un router è uno switch ma con funzionalità diverse.
>[!note] Switch
>Si occupa del trasferimento dall'interfaccia di input all'interfaccia di output.

- **Link Layer Switch** se l'inoltro avviene in relazione al valore del campo nel livello di collegamento (livello 2)
- **Router** se l'inoltro avviene in relazione al valore del campo nel livello di rete (livello 3)

>[!note] Link Layer Switch
>Utilizzato per collegare i singoli computer all'interno di una rete LAN

### Switching
>[!note] Approccio a circuito virtuale
>I due sistemi terminali instaurano prima una connessione (servizio orientato alla connessione)
>
>Viene utilizzata un'etichetta di circuito all'interno della tabella per indicare l'interfaccia di uscita e la virtual circuit d'uscita.


