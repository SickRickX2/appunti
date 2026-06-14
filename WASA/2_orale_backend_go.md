# Guida all'Orale – Backend Go

## Architettura generale

Il backend è strutturato in tre livelli che non si "parlano" mai direttamente, ma passano attraverso interfacce:

```
HTTP Request
     ↓
cmd/webapi/main.go      ← punto di ingresso, mette tutto insieme
     ↓
service/api/            ← LIVELLO 1: router HTTP + handler (logica di business)
     ↓
service/database/       ← LIVELLO 2: interfaccia con il database SQLite
     ↓
SQLite (file .db)       ← LIVELLO 3: dati persistenti
```

### Perché questa separazione?

È un principio chiamato **Separation of Concerns**: ogni livello ha una sola responsabilità. Se domani vogliamo cambiare SQLite con PostgreSQL, modifichiamo solo `service/database/` senza toccare gli handler. Se vogliamo cambiare un'API, modifichiamo solo `service/api/` senza toccare il DB.

---

## Come funziona `httprouter`

`httprouter` è la libreria che associa un URL a una funzione Go. In `service/api/api-handler.go`:

```go
rt.router.POST("/session", rt.doLogin)
rt.router.GET("/conversations/:convId/messages", rt.getMessages)
```

Quando arriva una richiesta HTTP `POST /session`, `httprouter` chiama automaticamente `rt.doLogin`. I parametri nel path (come `:convId`) vengono estratti con `ps.ByName("convId")`.

Ogni handler ha sempre questa firma:
```go
func (rt *_router) nomeHandler(w http.ResponseWriter, r *http.Request, ps httprouter.Params)
```
- `w` è dove scrivi la risposta (status code + body)
- `r` è la richiesta in arrivo (header, body, query params)
- `ps` sono i parametri del path (`:convId`, `:messageId`, ecc.)

---

## L'interfaccia `AppDatabase`

In `service/database/database.go` è definita l'interfaccia:

```go
type AppDatabase interface {
    CreateUser(u schemas.User) error
    FindUserByName(name string) (schemas.User, error)
    ReactToMessage(messageId schemas.MessageId, userId schemas.UserId, emoji string) error
    // ... tutti i metodi del DB
    Ping() error
}
```

Gli handler nel livello `service/api/` accedono al DB solo attraverso questa interfaccia, tramite `rt.db.NomeMetodo(...)`. Non sanno nulla di SQL. Questo è il pattern **Repository** o **Data Access Object**.

---

## Il flow di una richiesta: esempio `sendMessage`

Seguiamo passo per passo cosa succede quando l'utente manda un messaggio (`POST /conversations/{convId}/messages`):

**Step 1 – Autenticazione** (righe 17-27 di `post-message.go`)
```go
authHeader := r.Header.Get("Authorization")
parts := strings.Split(authHeader, " ")
// parts[0] = "Bearer", parts[1] = "usr_a1B2c3"
senderId := schemas.UserId(parts[1])
```
Il backend legge l'header, estrae il token (che è l'userId) e lo usa per sapere chi sta scrivendo.

**Step 2 – Estrazione parametri path**
```go
convId := schemas.ConversationId(vars.ByName("convId"))
```
Prende `convId` dall'URL.

**Step 3 – Parsing del body JSON**
```go
var req struct {
    Text      string         `json:"text"`
    Media     *schemas.Media `json:"media,omitempty"`
    ReplyToId *schemas.MessageId `json:"replyToId,omitempty"`
}
json.NewDecoder(r.Body).Decode(&req)
```
Decodifica il JSON in arrivo in una struct Go. Il `json:"text"` è il "tag": dice quale chiave JSON corrisponde a quale campo Go.

**Step 4 – Validazioni**
```go
if req.Text == "" && mediaId == "" {
    http.Error(w, "Message must contain either text or media", http.StatusBadRequest)
    return
}
```
Controlla che il messaggio non sia vuoto. Se fallisce, risponde subito con 400 e interrompe l'esecuzione con `return`.

**Step 5 – Controllo autorizzazione**
```go
isInConversation, err := rt.db.IsUserInConversation(convId, senderId)
if !isInConversation {
    http.Error(w, "Bad request", http.StatusBadRequest)
    return
}
```
Verifica che l'utente faccia effettivamente parte di quella conversazione prima di permettergli di scrivere.

**Step 6 – Creazione e salvataggio**
```go
newMessage := schemas.Message{
    ID:     generateMessageId(), // genera "msg_xxxxxxxxxxxx"
    Sender: senderId,
    Text:   req.Text,
    Time:   time.Now(),
    Status: schemas.MsgStatusDelivered,
    Kind:   "normal",
}
rt.db.CreateMessage(convId, newMessage)
```

**Step 7 – Risposta**
```go
w.WriteHeader(http.StatusNoContent) // 204
```
Nessun body, solo il codice di stato.

---

## Analisi di un requisito complesso: Inoltro di un messaggio

File: `service/api/post-forward-message.go`

Il forward deve:
1. Verificare che l'utente sia nella chat di **origine** (da cui preleva il messaggio)
2. Verificare che l'utente sia nella chat di **destinazione** (dove manda il messaggio)
3. Copiare il contenuto del messaggio originale in un nuovo messaggio
4. Salvare il nuovo messaggio con `Kind: "forwarded"`

```go
// 1. Estrai il messaggio originale
originalMsg, err := rt.db.GetMessage(originalMessageId)

// 2. Crea una COPIA (non uno spostamento)
forwardedMsg := schemas.Message{
    ID:      generateMessageId(), // nuovo ID univoco
    Sender:  userId,              // il mittente è CHI sta inoltrando, non l'autore originale
    Text:    originalMsg.Text,    // stesso testo
    MediaId: originalMsg.MediaId, // stessa immagine (se c'era)
    Time:    time.Now(),          // timestamp ATTUALE
    Status:  "sent",
    Kind:    "forwarded",         // ← questo è il marker che vede User C
}

// 3. Salvalo nella chat di destinazione
rt.db.CreateMessage(req.DestinationConvId, forwardedMsg)
```

Il campo `Kind: "forwarded"` è quello che il frontend legge per mostrare l'etichetta "Forwarded ↪".

---

## Analisi di un requisito complesso: Reazioni

File: `service/api/reactions.go` e `service/database/reactions.go`

La logica del DB è elegante:
```sql
INSERT OR REPLACE INTO message_reactions (messageId, userId, emoji)
VALUES (?, ?, ?)
```

`INSERT OR REPLACE` è una feature di SQLite: se esiste già una riga con la stessa chiave primaria `(messageId, userId)`, la sostituisce. Questo implementa automaticamente la policy "un utente può avere una sola reazione per messaggio" — se cambi emoji, la vecchia viene sovrascritta.

L'handler Go fa:
1. Verifica che l'utente sia nella conversazione
2. Verifica che il messaggio esista in quella conversazione
3. Chiama `db.ReactToMessage(messageId, userId, emoji)` che esegue l'`INSERT OR REPLACE`
4. Rilegge il messaggio aggiornato e lo manda come risposta

---

## Analisi di un requisito complesso: Mark as Seen (doppie spunte blu)

File: `service/api/put-seen.go` e `service/database/mark-seen.go`

```go
// Handler (put-seen.go)
updatedMsg, err := rt.db.MarkAsSeen(convId, messageId, userId)
```

Nel DB (`mark-seen.go`), l'operazione è in due passi atomici:
1. Inserisce una riga in `message_reads` (tabella che tiene traccia di chi ha letto cosa)
2. Aggiorna lo `status` del messaggio a `"seen"` nella tabella `messages`

La tabella `message_reads` ha chiave primaria `(messageId, userId)`, quindi ogni utente viene registrato una sola volta per messaggio. Per le chat private, quando l'altro utente legge, il messaggio diventa "seen". Per i gruppi, la logica delle spunte blu è gestita lato frontend (conta quanti partecipanti hanno letto).

---

## Il CORS: cos'è e come lo abbiamo risolto

**Cos'è il CORS?** È una policy di sicurezza dei browser. Se il tuo frontend gira su `localhost:8080` e chiama il backend su `localhost:3000`, il browser blocca la richiesta perché l'**origine** è diversa (porta diversa = origine diversa). Questo protegge gli utenti da attacchi dove una pagina malevola fa richieste ad altri siti a loro nome.

**Come lo abbiamo risolto** (in `cmd/webapi/cors.go`):
```go
return handlers.CORS(
    handlers.AllowedHeaders([]string{"Authorization", "Content-Type"}),
    handlers.AllowedMethods([]string{"GET", "POST", "OPTIONS", "DELETE", "PUT"}),
    handlers.AllowedOrigins([]string{"*"}), // accetta da qualsiasi origine
    handlers.MaxAge(1),
)(h)
```

Il middleware `gorilla/handlers` aggiunge automaticamente gli header HTTP `Access-Control-Allow-*` alle risposte. Quando il browser vede questi header, permette al JavaScript del frontend di leggere la risposta. `AllowedOrigins: ["*"]` significa "accetta richieste da qualsiasi dominio" — in produzione si restringerebbe al dominio specifico.

Il middleware viene applicato in `main.go` dopo aver creato il router:
```go
router = applyCORSHandler(router)
```

---

## Lo schema del database

Il database viene creato automaticamente al primo avvio, in `service/database/database.go`. Non ci sono file di migrazione separati: il codice Go crea le tabelle se non esistono.

Le tabelle principali e le relazioni:
- `users` → `conversation_participants` → `conversations` (many-to-many)
- `conversations` → `messages` (one-to-many)
- `messages` → `message_reads` (chi ha letto cosa)
- `messages` → `message_reactions` (reazioni per messaggio)
- `media` → referenziata dai messaggi tramite `mediaId`

---

## Possibili domande d'esame

**D: Come funziona l'autenticazione nel backend?**
R: Ogni handler legge l'header `Authorization: Bearer <userId>`. Non c'è un middleware centralizzato — ogni handler esegue la verifica manualmente estraendo il token con `strings.TrimPrefix(authHeader, "Bearer ")`. L'userId estratto viene poi usato come identità dell'utente per tutte le operazioni successive.

**D: Perché usi un'interfaccia (`AppDatabase`) invece di usare direttamente il database?**
R: Perché le interfacce in Go permettono il disaccoppiamento. Gli handler non sanno e non vogliono sapere se il database è SQLite, PostgreSQL o un mock in memoria. Questo rende il codice testabile (si può iniettare un fake database) e sostituibile senza cambiare la logica di business.

**D: Cosa succede se due utenti si registrano con lo stesso nome nello stesso momento (race condition)?**
R: La colonna `userName` nella tabella `users` ha il vincolo `UNIQUE`. Se due inserimenti concorrenti provano a creare lo stesso nome, SQLite garantisce che solo uno vada a buon fine. Il codice in `post-session.go` prima cerca l'utente per nome con `FindUserByName`; se non lo trova, lo crea. In caso di collisione, il secondo inserimento fallirà e il codice ha un meccanismo di retry (fino a 3 tentativi con ID diversi).

**D: Come hai gestito la policy "un utente, una reazione per messaggio"?**
R: A livello di database, con `INSERT OR REPLACE` su una tabella che ha chiave primaria composta `(messageId, userId)`. SQLite gestisce automaticamente la sostituzione: se l'utente aveva già messo 👍 e ora mette ❤️, la riga viene sovrascritta. Non serve nessuna logica applicativa aggiuntiva.

**D: Cosa significa "soft delete" per i messaggi?**
R: Invece di eseguire un `DELETE` SQL, l'handler aggiorna il campo `status` del messaggio a `"deleted"`. Il messaggio rimane nel database ma il frontend lo visualizza come "This message has been deleted". Questo mantiene la coerenza della cronologia della chat per tutti i partecipanti.
