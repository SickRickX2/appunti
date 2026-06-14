# Guida all'Orale – Le Funzioni Principali del Progetto

Riferimento rapido: cosa fa ogni funzione importante, dove si trova, perché esiste.

---

## BACKEND (Go)

---

### `run()` — `cmd/webapi/main.go`

**Il cuore dell'avvio del server.** È la prima funzione chiamata. In ordine:
1. Carica la configurazione (porta, percorso DB, debug mode)
2. Inizializza il logger (`logrus`)
3. Apre la connessione SQLite
4. Crea il router API (`api.New(...)`)
5. Applica il middleware CORS
6. Avvia il server HTTP su `0.0.0.0:3000`
7. Rimane in ascolto di un segnale di terminazione (`SIGTERM`, `Ctrl+C`) per spegnersi in modo pulito

```go
func run() error { ... }
```

---

### `Handler()` — `service/api/api-handler.go`

**La mappa di tutto il backend.** Registra ogni route sul router associandola alla sua funzione handler. È il punto di riferimento per capire quali URL esistono e quale funzione li gestisce.

```go
rt.router.POST("/session", rt.doLogin)
rt.router.GET("/conversations/:convId/messages", rt.getMessages)
// ...e tutte le altre
```

Leggere questo file è il modo più rapido per avere una visione globale dell'API.

---

### `doLogin()` — `service/api/post-session.go`

**Il login/registrazione in un unico endpoint.** Implementa la logica "se esiste ritorna l'ID, se non esiste crealo":
1. Decodifica il body JSON (`{"name": "Pippo"}`)
2. Valida il nome (lunghezza, caratteri permessi)
3. Chiama `db.FindUserByName()` — se lo trova, restituisce il suo ID
4. Se non lo trova, genera un nuovo ID con `generateUserId()` e chiama `db.CreateUser()`
5. Risponde `201` con `{"identifier": "usr_xxxx"}`

```go
func (rt *_router) doLogin(w http.ResponseWriter, r *http.Request, ps httprouter.Params)
```

---

### `generateUserId()` e `generateMessageId()` — `post-session.go` e `post-message.go`

**I generatori di ID univoci.** Producono stringhe casuali rispettando i pattern dell'API:
- userId: `usr_` + 8 caratteri casuali → `usr_a1B2c3Xz`
- messageId: `msg_` + 10 caratteri casuali → `msg_a1B2c3Xz4Y`

I caratteri sono scelti dall'alfabeto `[A-Za-z0-9_-]` usando `rand.Intn`. La rarissima possibilità di collisione è gestita con un meccanismo di retry (max 3 tentativi).

---

### `sendMessage()` — `service/api/post-message.go`

**L'handler più rappresentativo del progetto.** Mostra il pattern completo di un handler Go:
1. Estrai l'userId dall'header `Authorization`
2. Estrai `convId` dal path
3. Decodifica il body JSON
4. Valida (testo non vuoto, max 150 char, testo o media obbligatorio)
5. Verifica che la conversazione esista
6. Verifica che l'utente sia membro della conversazione
7. Se c'è un mediaId, verifica che il media esista
8. Costruisce la struct `Message` e la salva nel DB
9. Risponde `204 No Content`

---

### `forwardMessage()` — `service/api/post-forward-message.go`

**L'inoltro messaggio.** Il punto chiave: crea una *copia* del messaggio (non lo sposta), con un nuovo ID, timestamp attuale, mittente = chi inoltra, e `Kind: "forwarded"`. Controlla che l'utente sia membro sia della chat sorgente che di quella di destinazione prima di procedere.

---

### `commentMessage()` / `uncommentMessage()` — `service/api/reactions.go`

**Aggiunta e rimozione reazioni.** `commentMessage` valida che l'emoji abbia tra 1 e 4 caratteri Unicode (non byte! Usa `utf8.RuneCountInString`), poi delega a `db.ReactToMessage()`. `uncommentMessage` delega a `db.UnreactToMessage()`. Entrambi rispondono con il messaggio aggiornato (non solo un `200 OK` vuoto) così il client può aggiornare la UI senza rifetchare.

---

### `markAsSeen()` — `service/api/put-seen.go`

**Le spunte blu.** Verifica che l'utente sia nella conversazione, poi chiama `db.MarkAsSeen()` che fa due cose: inserisce una riga in `message_reads` (per tenere traccia di chi ha letto) e aggiorna `status = 'seen'` nella tabella `messages`.

---

### `applyCORSHandler()` — `cmd/webapi/cors.go`

**Il middleware CORS.** Avvolge l'intero router con il middleware `gorilla/handlers` che aggiunge automaticamente gli header `Access-Control-Allow-*` a ogni risposta. Permette richieste da qualsiasi origine (`*`) e autorizza gli header `Authorization` e `Content-Type`. Senza questa funzione, il browser bloccherebbe tutte le richieste del frontend.

---

### `New()` — `service/database/database.go`

**Il costruttore del database.** Riceve una connessione `*sql.DB` già aperta e controlla l'esistenza di ogni tabella (`users`, `conversations`, `messages`, `conversation_participants`, `media`, `message_reads`, `message_reactions`). Se una tabella non esiste la crea con il suo `CREATE TABLE`. Nessun file di migrazione esterno: tutto è inline nel codice Go.

---

### `ReactToMessage()` — `service/database/reactions.go`

**Una riga di SQL che fa tutto.** Usa `INSERT OR REPLACE` che in SQLite significa: se esiste già una riga con la stessa chiave primaria `(messageId, userId)` la sostituisce, altrimenti la inserisce. Questo implementa automaticamente la policy "una reazione per utente per messaggio" senza nessuna logica applicativa aggiuntiva.

```sql
INSERT OR REPLACE INTO message_reactions (messageId, userId, emoji) VALUES (?, ?, ?)
```

---

## FRONTEND (Vue 3)

---

### `state` — `src/services/state.js`

**Lo stato globale dell'app.** Un oggetto `reactive` esportato che contiene `userId`, `userName` e `profilePictureUrl`. È il sostituto di Pinia: qualsiasi componente che importa `state` e legge `state.userId` si aggiorna automaticamente quando il valore cambia. `profilePictureUrl` è l'unico campo persistito in `localStorage` per sopravvivere al refresh.

---

### `resolveApiBaseUrl()` e l'interceptor — `src/services/axios.js`

**Due responsabilità in un file.** `resolveApiBaseUrl()` decide a quale indirizzo mandare le richieste API: usa `VITE_API_URL` se impostato a build time, altrimenti usa la stessa origine del browser (fondamentale per Docker). L'**interceptor** aggiunge automaticamente `Authorization: Bearer <userId>` a ogni richiesta, così nessun componente deve ricordarselo.

---

### `router.beforeEach()` — `src/router/index.js`

**Il guardiano delle route.** Eseguito prima di ogni navigazione. Implementa due regole: se l'utente non è autenticato e prova ad andare su qualsiasi pagina che non sia `/login`, viene reindirizzato al login. Se è già autenticato e prova ad andare su `/login`, viene reindirizzato alla home. È l'intera logica di protezione dell'app.

---

### `loadConversations()` — `src/views/HomeView.vue`

**Il refresh della sidebar.** Chiama `GET /users/{userId}/conversations`, aggiorna il ref reattivo `conversations`, poi in background:
- chiama `loadGroupPhotos()` per caricare le foto dei gruppi
- chiama `loadParticipantPfps()` per caricare le foto profilo degli altri utenti
- chiama `enrichConversationNames()` per popolare la cache nome→userId

È chiamata sia all'avvio che ogni 3 secondi dal polling.

---

### `loadMessages()` — `src/views/HomeView.vue`

**Il caricamento dei messaggi della chat aperta.** Chiama `GET /conversations/{id}/messages?limit=20&offset=0`, aggiorna `currentMessages`, risolve i nomi dei mittenti, scrolla in fondo se necessario, e poi chiama `markUnreadMessagesAsSeen()`. Ha opzioni per distinguere il caricamento iniziale dal polling, per non mostrare lo spinner ad ogni aggiornamento automatico.

---

### `syncData()` — `src/views/HomeView.vue`

**Il polling intelligente.** Invece di ricaricare tutto ogni 3 secondi (che causerebbe un flash visivo), confronta i messaggi già in memoria con quelli appena scaricati e aggiunge solo quelli nuovi. Usa un `Set` di ID già presenti per trovare i nuovi in O(1).

```javascript
const existingIds = new Set(currentMessages.value.map(m => m.messageId))
const newMessages = latestMessages.filter(m => !existingIds.has(m.messageId))
```

---

### `sendMessage()` — `src/views/HomeView.vue`

**L'invio di un messaggio.** Se c'è un file allegato, prima carica il media con `POST /media` e ottiene l'URL. Poi invia il messaggio con `POST /conversations/{id}/messages` includendo testo, eventuale media e eventuale `replyToId`. Dopo il successo, svuota il campo di testo, rimuove l'anteprima del file, cancella il contesto di risposta e ricarica i messaggi.

---

### `toggleReaction()` — `src/views/HomeView.vue`

**La reazione con ottimistic update.** È la funzione più complessa del frontend. Prima di fare la chiamata API, aggiorna immediatamente l'array `message.reactions` in memoria (così la UI risponde istantaneamente al click). Se la chiamata API fallisce, ripristina lo stato precedente (`backupReactions`). Questo pattern si chiama **optimistic update** ed è ciò che rende la UI reattiva senza aspettare il server.

---

### `markUnreadMessagesAsSeen()` — `src/views/HomeView.vue`

**Le spunte automatiche.** Filtra i messaggi non miei e non ancora visti, poi chiama `PUT /conversations/{id}/messages/{id}/seen` per ognuno. Usa un `Set` locale (`locallyMarkedAsSeen`) per evitare di mandare la stessa richiesta due volte in caso di polling rapido.

---

### `ensureUserPfpLoaded()` — `src/views/HomeView.vue`

**Il caricamento lazy delle foto profilo.** Mantiene una cache `userPfpCache` (oggetto reattivo). Alla prima chiamata per un userId sconosciuto, fa `GET /users/{id}/pfp` e salva il risultato. Alle chiamate successive, restituisce dalla cache senza fare rete. Con `forceRefresh = true` (usato dal polling), non azzera la cache prima di ricevere la nuova foto — questo previene il flickering visivo.

---

### `executeForwardToUser()` — `src/views/HomeView.vue`

**Il forward verso un utente senza chat preesistente.** Cerca se esiste già una conversazione privata con quell'utente nella lista locale. Se sì, la riusa. Se no, chiama `POST /conversations` con `recipientId` per crearla, poi chiama `executeForward()` con il `convId` ottenuto.

---

### `aggregateReactions()` — `src/views/HomeView.vue`

**Il raggruppamento delle reazioni per emoji.** Il backend restituisce le reazioni come lista piatta (`[{userId, emoji}, {userId, emoji}]`). Questa funzione le aggrega per emoji producendo `[{emoji: "👍", count: 3, users: ["Alice", "Bob", "Carlo"]}]`. Il risultato viene passato a `MessageBubble` per il rendering visivo.

---

### `MessageBubble.vue` — `src/components/MessageBubble.vue`

**Il componente più riutilizzato.** Riceve un oggetto `message` e decide come renderizzarlo: bolla blu (mia) o bianca (altrui), testo o immagine, bolla barrata se `status === 'deleted'`, etichetta "Forwarded ↪" se `kind === 'forwarded'`, anteprima del messaggio citato se `replyToId` è presente, badge reazioni, timestamp, spunta singola o doppia (blu). Emette eventi (`forward-message`, `reply-message`, ecc.) invece di fare azioni direttamente — è `HomeView` che decide cosa fare.
