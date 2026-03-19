## Esito generale

**Compliancy OpenAPI: [FAIL]** (diverse discrepanze su path, status code, header e coverage endpoint).

---

## 1) Discrepanze di copertura routing vs `api.yaml`

- **[FAIL]** `GET /users/{userId}/pfp` **mancante** (YAML lo definisce).
- **[FAIL]** `DELETE /users/{userId}/pfp` **mancante** (YAML lo definisce).
- **[FAIL]** [GET /conversations/{convId}](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) **mancante**.
- **[FAIL]** [GET /users/{userId}/conversations](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) **mancante**.
- **[FAIL]** `DELETE /conversations/{convId}/participants/me` non presente: backend espone [.../participants/:userId](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html).
- **[FAIL]** Endpoint extra non in YAML: `GET /liveness`, [GET /images/*filepath](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html).

---

## 2) Checklist handler-by-handler

### Sessione

- **`doLogin` (`POST /session`)** → **[FAIL]**
    
    - Status `201` corretto.
    - **Header FAIL**: [Content-Type](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) impostato **dopo** `WriteHeader`.
    - Error handling encode non verificato ([_ = Encode(...)](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html)).
- **`logout` (`DELETE /session`)** → **[FAIL]**
    
    - Status `204` corretto.
    - **Input/Auth FAIL**: YAML richiede BearerAuth; handler non valida Authorization.

---

### Utenti

- **`setUsername` (`PUT /users/{userId}/username`)** → **[PASS]** (con riserva)
    
    - Path/input coerenti.
    - [Content-Type](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) corretto per risposta JSON.
    - Status `200` implicito.
    - Riserva: ritorna `500` in casi DB non documentati nello YAML estratto.
- **`setUserPhoto` (`PUT /users/{userId}/pfp`)** → **[FAIL]**
    
    - **Status FAIL**: YAML indica `200`, handler restituisce `204`.
    - Path/input ok.
    - Endpoint GET/DELETE pfp assenti (vedi copertura).
- **`searchUsers` ([GET /users](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html))** → **[FAIL]**
    
    - Header JSON presente.
    - **errcheck FAIL**: encode ignorato ([_ = Encode(users)](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html)).
    - Possibile mismatch payload (YAML non esplicita shape, handler ritorna array diretto).

---

### Conversazioni/Gruppi

- **`createConversation` ([POST /conversations](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html))** → **[PASS]** (con riserva)
    
    - `201` + JSON + header corretti.
    - Riserva: errori sempre `500` lato DB (YAML poco esplicito).
- **`createGroup` (`POST /groups`)** → **[PASS]**
    
    - `201`, header e JSON corretti.
- **`addToGroup` (`POST /conversations/{convId}/participants`)** → **[FAIL]**
    
    - Status `200` ok.
    - **Payload FAIL potenziale**: nessun body, mentre contratto tipicamente prevede risorsa aggiornata (YAML qui non dettagliato).
    - Auth minima (non estrae userId dal token), possibile gap di controllo.
- **`removeFromGroup` ([DELETE /conversations/{convId}/participants/:userId](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html))** → **[FAIL]**
    
    - **Path FAIL**: YAML vuole `/participants/me`.
    - **Status FAIL**: YAML indica `200`, handler `204`.
- **`setGroupPhoto` (`PUT /conversations/{convId}/group_photo`)** → **[FAIL]**
    
    - **Status FAIL**: YAML `200`, handler `204`.
- **`setGroupName` (`PUT /conversations/{convId}/group_name`)** → **[PASS]**
    
    - `200` + JSON + header corretti.
- **`getConversations` ([GET /conversations](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html))** → **[FAIL]**
    
    - **Path FAIL** rispetto YAML (che espone [/conversations/{convId}](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) e [/users/{userId}/conversations](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html)).
    - Payload wrapper [{ "conversations": [...] }](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) ben formato, ma endpoint non combacia.

---

### Messaggi

- **`getMessages` (`GET /conversations/{convId}/messages`)** → **[PASS]** (con riserva)
    
    - Header JSON corretto, status `200` implicito.
    - Riserva: payload è array diretto; YAML estratto non specifica schema response.
- **`sendMessage` (`POST /conversations/{convId}/messages`)** → **[FAIL]**
    
    - Status successo `204` coerente.
    - **Input FAIL**: usa [mediaId](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) flat; schema `Message` in YAML suggerisce `media` object.
    - Error mapping molto generico (`400` anche per errori DB/autorizzazione).
- **`deleteMessage` ([DELETE /conversations/{convId}/messages/{messageId}](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html))** → **[FAIL]** (probabile)
    
    - Restituisce JSON [updatedMsg](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) con `200`.
    - YAML estratto non definisce chiaramente risposta; in molti contratti delete è `204`.
    - Ambiguità ma non allineamento dimostrabile al 100%.
- **`forwardMessage` (`POST /.../forwarded`)** → **[PASS]** (con riserva)
    
    - `201`, header JSON, body presente.
    - Riserva: dipende da schema response effettivo nel YAML completo.
- **`markAsSeen` (`PUT /.../seen`)** → **[PASS]** (con riserva)
    
    - Header e status `200` coerenti.
    - Body `{ "success": true }` non verificabile senza schema response esplicito.

---

### Reazioni

- **`commentMessage` (`PUT /.../reaction`)** → **[FAIL]**
    
    - OperationId aggiornato ok.
    - Header JSON ok, status `200` implicito.
    - **Path/Input FAIL**: [convId](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) nel path non viene usato/validato.
    - **Status FAIL**: usa `500` non documentato nel YAML estratto.
    - Validazione emoji su byte-length ([len](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html)) non robusta per Unicode.
- **`uncommentMessage` (`DELETE /.../reaction`)** → **[FAIL]**
    
    - OperationId aggiornato ok.
    - Header JSON ok, status `200` implicito.
    - **Path/Input FAIL**: [convId](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) non usato.
    - **Status FAIL**: usa `500` non documentato nel YAML estratto.

---

### Media

- **`uploadMedia` (`POST /media`)** → **[PASS]** (con riserva)
    - `201`, header JSON prima di `WriteHeader`, payload JSON coerente ([mediaId](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html), `url`).
    - Riserva: requestBody in YAML estratto è poco specifico, quindi campo multipart ["file"](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html) non verificabile formalmente.

---

## 3) Problemi trasversali rilevanti

- **Header ordering**: in `doLogin` ordine errato (`WriteHeader` prima di `Header().Set`).
- **errcheck**: encode/write non sempre controllati (`doLogin`, `searchUsers`).
- **Error contract**: diversi handler ritornano `500` non documentato nello YAML estratto.
- **Path params non sfruttati**: reazioni ignorano [convId](vscode-file://vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-browser/workbench/workbench.html).

---
## Checklist operativa **file per file** 

Obiettivo: allineare `service/api/*` a api.yaml (OpenAPI 3.1), con priorità P0→P2.

---

### P0 — Bloccanti compliance

#### api-handler.go
- [x] Allineare route mancanti:
  - [x] Aggiungere `GET /users/:userId/pfp`
  - [x] Aggiungere `DELETE /users/:userId/pfp`
  - [x] Aggiungere `GET /conversations/:convId`
  - [x] Aggiungere `GET /users/:userId/conversations`
- [x] Allineare leave-group:
  - [x] Sostituire `DELETE /conversations/:convId/participants/:userId` con `DELETE /conversations/:convId/participants/me`
- [x] Verificare endpoint extra (`/liveness`, `/images/*filepath`): mantenerli solo se documentati o interni.

#### put-user-photo.go
- [x] Cambiare successo da `204` a `200` come da YAML.
- [x] Verificare payload di risposta conforme allo schema previsto (`User` o payload definito in YAML).

#### set-group-photo.go
- [x] Cambiare successo da `204` a `200`.
- [x] Verificare payload risposta conforme a YAML.

#### delete-group-participant.go
- [x] Adeguare handler al path `/participants/me` (target user = utente autenticato).
- [x] Allineare status successo a quello definito in YAML (atteso `200` nella tua spec corrente).
- [x] Verificare body di risposta se richiesto dallo schema.

#### Nuovi file handler (se mancanti)
- [x] Creare handler per `GET /users/:userId/pfp`.
- [x] Creare handler per `DELETE /users/:userId/pfp`.
- [x] Creare handler per `GET /conversations/:convId`.
- [x] Creare handler per `GET /users/:userId/conversations`.

---

### P1 — Mismatch funzionali importanti

#### post-message.go
- [x] Allineare request body a schema OpenAPI (`Message`): verificare uso `media` object vs `mediaId` string.
- [x] Mappare errori con status coerenti (`400/404/...`) invece di fallback generico.
- [x] Mantenere controlli `errcheck` su encode/write.

#### reactions.go
- [x] In `commentMessage` e `uncommentMessage`, usare/validare anche `convId` (non solo `messageId`).
- [x] Allineare status error ai codici documentati in YAML (evitare `500` se non previsto).
- [x] Verificare validazione emoji coerente con lunghezza logica (non byte-length pura).

#### delete-session.go
- [x] Enforce BearerAuth su `DELETE /session` (se richiesto da security globale YAML).

#### put-group-participants.go
- [ ] Verificare response body/status esatti da YAML per `POST /participants`.
- [ ] Aggiungere eventuali controlli membership/permessi coerenti con contratto.

#### delete-message.go
- [ ] Verificare status/body attesi dal YAML definitivo per `DELETE /messages/{messageId}`.
- [ ] Allineare output (es. `204` senza body vs `200` con body) in base alla spec.

---

### P2 — Qualità/consistenza/linter sta roba la posso pure scartare tanto non penso cambi realmente qualcosa

#### post-session.go
- [ ] Impostare `Content-Type` **prima** di `WriteHeader`.
- [ ] Non ignorare errori di `json.NewEncoder(...).Encode(...)`.

#### get-users.go
- [ ] Non ignorare errore di `Encode`.
- [ ] Verificare shape response (array diretto vs envelope) secondo schema YAML.

#### get-conversations.go
- [ ] Verificare se endpoint deve restare o essere sostituito dai 2 endpoint YAML specifici.
- [ ] Verificare shape response (`{conversations:[...]}` vs altro) contro schema.

#### get-messages.go
- [ ] Verificare shape response rispetto allo schema YAML (array/envelope).
- [ ] Confermare status code e header già corretti.

#### liveness.go
- [ ] Decidere: documentare in `api.yaml` o rimuovere dal perimetro pubblico.

#### upload-media.go
- [ ] Verificare nome field multipart (`file`) e schema response nel YAML definitivo.
- [ ] Confermare status `201` e `Content-Type` corretti.

---

## Criteri di accettazione finali (Definition of Done)
- [ ] Ogni path/metodo in `api.yaml` ha handler registrato e funzionante.
- [ ] Nessun endpoint pubblico non documentato (o esplicitamente marcato interno).
- [ ] Status code perfettamente allineati allo YAML.
- [ ] Header `Content-Type: application/json` impostato prima di `WriteHeader` quando c’è body JSON.
- [ ] Nessun `Encode/Write` ignorato dove `errcheck` è richiesto.
- [ ] Parametri path/query/body coerenti 1:1 con nomi e posizione in OpenAPI.