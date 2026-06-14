# Guida all'Orale – API REST (api.yaml)

## Cos'è un'API REST e perché la usiamo

REST (Representational State Transfer) è uno stile architetturale per progettare API su HTTP. L'idea fondamentale è che ogni **risorsa** (utente, conversazione, messaggio) ha un proprio URL, e si agisce su di essa usando i verbi standard di HTTP. Il vantaggio è che chiunque conosce HTTP capisce già come funziona la nostra API, senza dover leggere documentazione specifica.

---

## I verbi HTTP e come li abbiamo usati

| Verbo | Semantica | Esempio nel progetto |
|---|---|---|
| `GET` | Leggi, non modificare mai | `GET /conversations/{convId}/messages` |
| `POST` | Crea una nuova risorsa | `POST /conversations`, `POST /groups` |
| `PUT` | Sostituisci/aggiorna una risorsa esistente | `PUT /users/{userId}/username` |
| `DELETE` | Elimina/rimuovi | `DELETE /conversations/{convId}/messages/{messageId}` |

La regola d'oro: le operazioni `GET` sono **idempotenti e sicure** (ripeterle non cambia nulla). Le `PUT` sono **idempotenti** (ripeterle porta allo stesso risultato). Le `POST` non lo sono (ogni chiamata può creare qualcosa di nuovo).

**Eccezione notevole nel progetto:** `POST /conversations` è stata resa idempotente appositamente: se chiami questo endpoint due volte con lo stesso `recipientId`, non crea due conversazioni duplicate ma restituisce quella esistente. Questo è un pattern comune e corretto.

---

## Le risorse come URL gerarchici

Il design degli URL segue una gerarchia logica che rispecchia le relazioni tra le entità:

```
/users/{userId}                                → un utente specifico
/users/{userId}/conversations                  → le conversazioni di quell'utente
/conversations/{convId}/messages               → i messaggi di una conversazione
/conversations/{convId}/messages/{messageId}   → un messaggio specifico
/conversations/{convId}/messages/{messageId}/reaction  → la reazione su quel messaggio
```

Questo design è intuitivo: navigando l'URL da sinistra a destra, si scende nella gerarchia. Un professore chiederà spesso "perché hai messo la reazione come sotto-risorsa del messaggio?" — la risposta è: perché una reazione non esiste senza il messaggio a cui appartiene, è una risorsa dipendente.

---

## Autenticazione: il Bearer Token

Nel nostro sistema non usiamo JWT né sessioni lato server. L'autenticazione funziona così:

1. L'utente chiama `POST /session` con il suo nome
2. Il server risponde con un `identifier` (es. `usr_a1B2c3`)
3. Da quel momento, ogni richiesta include l'header: `Authorization: Bearer usr_a1B2c3`

**Perché proprio l'userId come token?** Perché il progetto non richiede sicurezza enterprise. L'userId è già unico, già generato dal server, e usarlo direttamente come token semplifica enormemente l'implementazione senza framework di sessioni. Il backend legge questo header, estrae l'ID e sa immediatamente chi sta facendo la richiesta.

L'unico endpoint che non richiede autenticazione è `POST /session` (ovviamente, perché è lì che ti autentichi). In `api.yaml` questo si esprime con `security: []` sull'operazione.

---

## Gli Status Code: perché contano

Usare il codice di stato giusto è la firma di un'API REST ben progettata.

### 201 Created
Usato quando si crea qualcosa di nuovo: `POST /session`, `POST /conversations`, `POST /groups`, `POST /media`, `POST /conversations/{id}/messages/{id}/forwarded`.
La regola: se la risorsa adesso esiste nel server e prima non esisteva, rispondi con 201.

### 200 OK
Usato quando l'operazione ha successo e c'è un body significativo da restituire ma non si è creata una nuova risorsa: `PUT /users/{id}/username`, `PUT /conversations/{id}/messages/{id}/reaction`, `GET` di qualsiasi risorsa. In pratica: "ho fatto quello che mi hai chiesto, eccoti il risultato".

### 204 No Content
Usato quando l'operazione ha successo ma non c'è nulla da restituire: `DELETE /session` (logout), e nel codice Go anche `POST /conversations/{id}/messages` (invio messaggio) restituisce 204. Il 204 dice esplicitamente "è andato tutto bene, ma non aspettarti dati in risposta".

### 400 Bad Request
Il client ha mandato qualcosa di malformato: JSON non valido, campo mancante, testo del messaggio troppo lungo. Non è un errore del server, è un errore di chi ha fatto la richiesta.

### 401 Unauthorized
Manca l'header `Authorization` o il token è malformato. Significa "non so chi sei".

### 403 Forbidden
So chi sei, ma non hai il permesso. Esempio: cerchi di cambiare la foto profilo di un altro utente. Differenza sottile ma importante con 401.

### 404 Not Found
La risorsa che cerchi non esiste: conversazione, messaggio, utente non trovati. Usato anche quando non si vuole rivelare l'esistenza di una risorsa protetta.

### 413 Payload Too Large
Specifico per l'upload di file: il file supera i 5MB.

---

## Soft Delete dei messaggi

Un'importante scelta di design: `DELETE /conversations/{convId}/messages/{messageId}` **non cancella fisicamente** il messaggio dal database. Imposta il campo `status` a `"deleted"` e restituisce il messaggio aggiornato con status 200. Il client mostra "This message has been deleted".

Perché? Perché cancellare fisicamente un messaggio crea problemi di integrità: gli altri utenti che lo vedevano già non devono vedere un buco nella conversazione. Con il soft delete tutti vedono il segnaposto.

---

## La paginazione dei messaggi

`GET /conversations/{convId}/messages` accetta i parametri `limit` e `offset` (nella nostra implementazione). Questo permette di caricare prima gli ultimi 20 messaggi, poi altri 20 scorrendo in su, invece di caricarli tutti in una volta (potenzialmente migliaia).

---

## Possibili domande d'esame

**D: Cos'è REST e quali principi hai applicato?**
R: REST è uno stile architetturale che usa HTTP in modo semantico. Ho applicato: risorse identificate da URL gerarchici, verbi HTTP con la loro semantica corretta (GET per leggere, POST per creare, PUT per aggiornare, DELETE per rimuovere), status code significativi, e un'API stateless dove ogni richiesta è autocontenuta e include il token di autenticazione.

**D: Perché `POST /session` risponde 201 anche se l'utente esiste già?**
R: Perché dal punto di vista del client si sta creando una sessione, che è una nuova risorsa. La logica "crea se non esiste, altrimenti recupera" è trasparente al client: lui vuole accedere al sistema e riceve un identificatore. Il 201 comunica che l'operazione di accesso è avvenuta con successo.

**D: Qual è la differenza tra 401 e 403?**
R: 401 significa "non so chi sei" (token mancante o non valido). 403 significa "so chi sei, ma non puoi farlo" (ad esempio, tentare di modificare il profilo di un altro utente).

**D: Perché hai scelto di fare il soft delete dei messaggi invece di cancellarli fisicamente?**
R: Per preservare la coerenza della conversazione per tutti i partecipanti. Un messaggio cancellato fisicamente creerebbe un buco nella storia della chat. Con il soft delete il messaggio rimane nel DB con `status: "deleted"` e il client mostra un segnaposto. È lo stesso approccio di WhatsApp.

**D: Cosa significa che `POST /conversations` è idempotente nonostante sia un POST?**
R: Tecnicamente i POST non sono tenuti a essere idempotenti, ma abbiamo scelto di renderlo tale per migliorare l'esperienza. Se chiami due volte l'endpoint con lo stesso `recipientId`, non crei due conversazioni: il server controlla se ne esiste già una e la restituisce. Questo previene duplicati anche in caso di doppio click o retry di rete.
