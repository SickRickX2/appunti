# Guida all'Orale – Scaletta delle Operazioni Principali

Per ogni operazione: cosa fa, come funziona nel backend, come il frontend la scatena, e i file da guardare.

---

## 1. `doLogin`
**Endpoint:** `POST /session`

**Cosa fa:** Login e registrazione in uno. Se l'utente esiste lo riconosce, altrimenti lo crea.

**Backend (`post-session.go`):**
1. Legge `{"name": "Pippo"}` dal body
2. Valida il nome (3–16 caratteri, solo `A-Za-z0-9_-`)
3. Cerca l'utente nel DB per nome → se esiste, prende il suo ID
4. Se non esiste, genera un nuovo `usr_xxxxxxxx` con caratteri casuali e lo inserisce nel DB (max 3 tentativi in caso di collisione)
5. Risponde `201` con `{"identifier": "usr_xxxxxxxx"}`

**Frontend (`LoginView.vue`):**
- L'utente scrive il nome e preme Login
- `axios.post('/session', { name })` → riceve l'identifier
- Salva `state.userId` e `state.userName`, scrive in `localStorage`
- Il router guard rileva che ora è autenticato e rimanda alla Home

**File:** `service/api/post-session.go`, `service/database/createuser.go`, `webui/src/views/LoginView.vue`

---

## 2. `setMyUserName`
**Endpoint:** `PUT /users/{userId}/username`

**Cosa fa:** Cambia il nome visualizzato dell'utente.

**Backend (`put-username.go`):**
1. Estrae l'userId dal token e lo confronta con quello nell'URL → se diversi risponde `403 Forbidden` (non puoi cambiare il nome di un altro)
2. Valida il nuovo nome (stesse regole del login)
3. Controlla che il nome non sia già usato da un altro utente con `CountUsersByNameExcludingUser`
4. Aggiorna il DB con `SetUserName`, rilegge l'utente aggiornato, risponde `200` con il profilo completo

**Frontend (`ConversationHeader.vue` o modale impostazioni):**
- L'utente modifica il campo nome nel proprio profilo
- `axios.put('/users/{userId}/username', { username: nuovoNome })`
- Aggiorna `state.userName` con il valore restituito

**File:** `service/api/put-username.go`, `service/database/set-name.go`

---

## 3. `getMyConversations`
**Endpoint:** `GET /users/{userId}/conversations`

**Cosa fa:** Carica la lista di tutte le chat dell'utente (private + gruppi), ognuna con l'anteprima dell'ultimo messaggio e il numero di non letti.

**Backend (`get-conversations.go`):**
1. Verifica che l'userId nel token corrisponda a quello nell'URL (non puoi vedere le chat altrui)
2. Chiama `db.GetConversations(userId)` → query SQL che fa JOIN tra `conversation_participants`, `conversations`, `messages` e `message_reads`
3. Risponde `200` con `{"conversations": [...]}`

**Frontend (`HomeView.vue`):**
- Chiamata in `loadConversations()`, eseguita all'avvio e ogni 3 secondi dal polling
- Il risultato aggiorna il ref reattivo `conversations` → la sidebar si ridisegna automaticamente
- Dopo il caricamento partono in background: `loadGroupPhotos()`, `loadParticipantPfps()`, `enrichConversationNames()`

**File:** `service/api/get-conversations.go`, `service/database/get-conversations.go`, `webui/src/views/HomeView.vue` → `loadConversations()`

---

## 4. `getConversation`
**Endpoint:** `GET /conversations/{convId}`

**Cosa fa:** Carica i dettagli di una singola conversazione (usato soprattutto per i gruppi e le loro foto).

**Backend (`get-conversation.go`):**
1. Verifica che l'utente sia membro di quella conversazione con `IsUserInConversation`
2. Chiama `db.GetConversation(convId)` che restituisce `any` (può essere `PrivateConversation` o `Group`)
3. Risponde `200` con i dettagli

**Frontend (`HomeView.vue`):**
- Chiamato in `loadGroupPhotos()` per aggiornare la foto dei gruppi nella sidebar
- Chiamato anche alla creazione di un gruppo per caricare subito la foto
- Il risultato va in `groupPhotoCache[convId]`

**File:** `service/api/get-conversation.go`, `service/database/get-conversation.go`, `webui/src/views/HomeView.vue` → `loadGroupPhotos()`

---

## 5. `sendMessage`
**Endpoint:** `POST /conversations/{convId}/messages`

**Cosa fa:** Invia un nuovo messaggio (testo, immagine, o entrambi) in una conversazione.

**Backend (`post-message.go`):**
1. Estrae sender dal token, `convId` dall'URL
2. Decodifica body: `text`, `media` (opzionale), `replyToId` (opzionale)
3. Valida: almeno uno tra testo e media, testo max 150 char
4. Verifica che la conversazione esista e che l'utente ne faccia parte
5. Se c'è un media, verifica che esista nel DB
6. Crea la struct `Message` con nuovo ID, `kind: "normal"`, `status: "delivered"`, timestamp ora
7. Salva nel DB → risponde `204 No Content`

**Frontend (`HomeView.vue`):**
- Se c'è un file allegato, prima `POST /media` per caricarlo e ottenere l'URL
- Poi `axios.post('/conversations/{id}/messages', { text, media, replyToId })`
- Dopo il successo chiama `loadMessages()` per aggiornare la chat

**File:** `service/api/post-message.go`, `service/database/create-message.go`, `webui/src/views/HomeView.vue` → `sendMessage()`

---

## 6. `forwardMessage`
**Endpoint:** `POST /conversations/{convId}/messages/{messageId}/forwarded`

**Cosa fa:** Copia un messaggio in un'altra conversazione, marcandolo come "inoltrato".

**Backend (`post-forward-message.go`):**
1. Verifica che l'utente sia nella chat **sorgente** (da cui preleva)
2. Verifica che l'utente sia nella chat **destinazione** (dove manda)
3. Recupera il messaggio originale
4. Crea una **copia** con nuovo ID, sender = chi inoltra, timestamp attuale, stesso testo/media, `kind: "forwarded"`
5. Salva nella chat di destinazione → risponde `201`

**Frontend (`HomeView.vue`):**
- Click su "Forward" → si apre il modale con lista chat + ricerca utenti
- Se si sceglie un utente senza chat esistente, `executeForwardToUser()` crea prima la conversazione con `POST /conversations`, poi chiama `executeForward()`
- `executeForward()` fa `axios.post('/conversations/{sourceId}/messages/{msgId}/forwarded', { destinationConversationId })`
- Dopo il successo naviga alla chat di destinazione

**File:** `service/api/post-forward-message.go`, `service/database/create-message.go`, `webui/src/views/HomeView.vue` → `executeForward()`, `executeForwardToUser()`

---

## 7. `commentMessage`
**Endpoint:** `PUT /conversations/{convId}/messages/{messageId}/reaction`

**Cosa fa:** Aggiunge o cambia la reazione emoji dell'utente su un messaggio.

**Backend (`reactions.go`):**
1. Verifica che l'utente sia nella conversazione e che il messaggio esista in essa
2. Valida l'emoji (1–4 caratteri Unicode)
3. `db.ReactToMessage()` esegue `INSERT OR REPLACE` → se l'utente aveva già una reazione la sovrascrive automaticamente
4. Rilegge il messaggio aggiornato e risponde `200` con esso

**Frontend (`HomeView.vue`):**
- `toggleReaction()` usa l'**optimistic update**: aggiorna subito l'array locale `message.reactions` prima della risposta API
- Se la chiamata fallisce, ripristina `backupReactions`
- `axios.put('/conversations/{id}/messages/{id}/reaction', { emoji })`

**File:** `service/api/reactions.go`, `service/database/reactions.go`, `webui/src/views/HomeView.vue` → `toggleReaction()`

---

## 8. `uncommentMessage`
**Endpoint:** `DELETE /conversations/{convId}/messages/{messageId}/reaction`

**Cosa fa:** Rimuove la reazione dell'utente da un messaggio.

**Backend (`reactions.go`):**
1. Stesse verifiche di `commentMessage`
2. `db.UnreactToMessage()` esegue `DELETE FROM message_reactions WHERE messageId=? AND userId=?`
3. Risponde `200` con il messaggio aggiornato

**Frontend (`HomeView.vue`):**
- Stesso `toggleReaction()` di sopra: se l'utente clicca sulla sua stessa emoji già messa, `isRemoving = true` e parte `axios.delete('/conversations/{id}/messages/{id}/reaction')`
- Stessa logica di optimistic update + rollback

**File:** `service/api/reactions.go`, `service/database/reactions.go`, `webui/src/views/HomeView.vue` → `toggleReaction()`

---

## 9. `deleteMessage`
**Endpoint:** `DELETE /conversations/{convId}/messages/{messageId}`

**Cosa fa:** Soft delete — non cancella fisicamente, imposta `status: "deleted"`.

**Backend (`delete-message.go`):**
1. Estrae userId dal token, `convId` e `messageId` dall'URL
2. `db.DeleteMessage()` verifica che il messaggio appartenga alla conversazione, che l'utente sia il mittente, poi aggiorna `status = 'deleted'` nel DB
3. Risponde `200` con il messaggio aggiornato (ora con status deleted)

**Frontend (`HomeView.vue`):**
- Click su "Delete" nel menu del messaggio → `confirm()` per sicurezza
- `axios.delete('/conversations/{id}/messages/{id}')`
- Aggiorna localmente il messaggio nell'array `currentMessages` con i dati ricevuti (non ricarica tutto)
- `MessageBubble` rileva `status === 'deleted'` e mostra "This message has been deleted"

**File:** `service/api/delete-message.go`, `service/database/delete-message.go`, `webui/src/views/HomeView.vue` → `deleteMessage()`, `webui/src/components/MessageBubble.vue`

---

## 10. `addToGroup`
**Endpoint:** `POST /conversations/{convId}/participants`

**Cosa fa:** Aggiunge uno o più utenti a un gruppo. Genera un messaggio di sistema visibile nella chat.

**Backend (`put-group-participants.go`):**
1. Verifica che chi aggiunge sia già membro del gruppo
2. Aggiunge gli utenti con `db.AddGroupMembers()`
3. Per ogni utente aggiunto crea un messaggio di sistema con `kind: "system_add_member"` nella chat (quello che dice "X ha aggiunto Y")
4. Risponde `200` con il gruppo aggiornato

**Frontend (`GroupInfoModal.vue` via `HomeView.vue`):**
- Nel modale info gruppo, l'utente cerca un nome → appare la lista utenti non ancora nel gruppo
- Click su un utente → `addUserToSelectedGroup(user)` in `HomeView`
- `axios.post('/conversations/{id}/participants', { userIds: [userId] })`
- Dopo il successo ricarica conversazioni e messaggi (il messaggio di sistema appare in chat)

**File:** `service/api/put-group-participants.go`, `service/database/add-member.go`, `webui/src/views/HomeView.vue` → `addUserToSelectedGroup()`, `webui/src/components/GroupInfoModal.vue`

---

## 11. `leaveGroup`
**Endpoint:** `DELETE /conversations/{convId}/participants/me`

**Cosa fa:** L'utente abbandona un gruppo. Genera un messaggio di sistema.

**Backend (`delete-group-participant.go`):**
1. Prima di rimuoversi, crea un messaggio di sistema `kind: "system_leave_group"` con il proprio nome come testo
2. Poi chiama `db.RemoveGroupMember()` che rimuove la riga da `conversation_participants`
3. Risponde `200` con il gruppo aggiornato (senza l'utente uscito)

**Frontend (`HomeView.vue`):**
- Pulsante "Leave group" nel `GroupInfoModal`
- `confirm()` di conferma, poi `axios.delete('/conversations/{id}/participants/me')`
- Chiude il modale, deseleziona la conversazione, svuota `currentMessages`, ricarica la lista chat

**File:** `service/api/delete-group-participant.go`, `service/database/remove-member.go`, `webui/src/views/HomeView.vue` → `leaveSelectedGroup()`

---

## 12. `setGroupName`
**Endpoint:** `PUT /conversations/{convId}/group_name`

**Cosa fa:** Cambia il nome del gruppo. Chiunque sia nel gruppo può farlo.

**Backend (`put-group-name.go`):**
1. Verifica che l'utente sia membro del gruppo
2. Valida il nome (1–30 caratteri)
3. `db.SetGroupName()` aggiorna la colonna `groupName` nella tabella `conversations`
4. Risponde `200` con il gruppo aggiornato

**Frontend (`GroupInfoModal.vue` via `HomeView.vue`):**
- Campo editabile nel modale info gruppo
- `handleUpdateGroupName(newName)` in `HomeView` → `axios.put('/conversations/{id}/group_name', { groupName })`
- Ricarica le conversazioni → la sidebar mostra il nuovo nome

**File:** `service/api/put-group-name.go`, `service/database/set-group-name.go`, `webui/src/views/HomeView.vue` → `handleUpdateGroupName()`

---

## 13. `setMyPhoto`
**Endpoint:** `PUT /users/{userId}/pfp`

**Cosa fa:** Imposta la foto profilo dell'utente. Richiede che il file sia già stato caricato prima con `POST /media`.

**Backend (`put-user-photo.go`):**
1. Verifica che l'userId del token corrisponda all'userId nell'URL (`403` se diversi)
2. Riceve `{"mediaId": "med_xxxxx"}` dal body (non il file direttamente)
3. Recupera l'URL del file dal DB con `GetMediaUrl(mediaId)`
4. Aggiorna `pfpUrl` nella tabella `users` con `SetUserPhoto()`
5. Risponde `200` con `{"pfpUrl": "/images/med_xxxxx.jpg"}`

**Frontend:**
- Flusso in due step: prima `POST /media` per caricare il file (ricevi `mediaId`), poi `PUT /users/{id}/pfp` con il `mediaId`
- Dopo il successo aggiorna `state.profilePictureUrl` e lo persiste in `localStorage`

**File:** `service/api/put-user-photo.go`, `service/api/upload-media.go`, `service/database/set-photo.go`

---

## 14. `setGroupPhoto`
**Endpoint:** `PUT /conversations/{convId}/group_photo`

**Cosa fa:** Imposta la foto del gruppo. A differenza della foto profilo, il file viene caricato direttamente in questo endpoint (non passa da `POST /media`).

**Backend (`set-group-photo.go`):**
1. Verifica che l'utente sia membro del gruppo
2. Riceve il file come `multipart/form-data` (max 5MB)
3. Legge i primi 512 byte per rilevare il MIME type e verificare che sia un'immagine
4. Salva il file su disco in `/images/` con un ID generato (`med_xxxxx.ext`)
5. Salva i metadati in tabella `media` nel DB
6. Aggiorna `groupPhoto` nella tabella `conversations`
7. Risponde `200` con il gruppo aggiornato

**Frontend (`GroupInfoModal.vue` via `HomeView.vue`):**
- L'utente seleziona un file nel modale del gruppo
- `handleUpdateGroupPhoto(file)` in `HomeView` → `axios.put('/conversations/{id}/group_photo', formData, { headers: multipart })`
- Ricarica le conversazioni → `groupPhotoCache` si aggiorna → la foto appare in sidebar e nell'header

**File:** `service/api/set-group-photo.go`, `service/database/set-group-photo.go`, `webui/src/views/HomeView.vue` → `handleUpdateGroupPhoto()`, `webui/src/components/GroupInfoModal.vue`
