# Guida all'Orale – Frontend Vue 3

## Struttura dell'app

```
webui/src/
├── main.js                  ← punto di ingresso: monta l'app
├── App.vue                  ← componente radice (contiene <RouterView>)
├── router/index.js          ← definisce le route e i guard di navigazione
├── services/
│   ├── axios.js             ← istanza axios configurata (base URL + auth header)
│   └── state.js             ← stato globale reattivo (userId, userName, pfp)
├── views/
│   ├── LoginView.vue        ← pagina di login
│   └── HomeView.vue         ← la vera app: sidebar + chat + modali
└── components/
    ├── MessageBubble.vue    ← singola bolla messaggio
    ├── ConversationsSidebar.vue ← lista chat a sinistra
    ├── ConversationHeader.vue   ← intestazione chat aperta
    ├── NewChatModal.vue         ← modale "nuova chat"
    ├── NewGroupModal.vue        ← modale "nuovo gruppo"
    ├── GroupInfoModal.vue       ← dettagli/gestione gruppo
    ├── UserAvatar.vue           ← avatar con lettera o foto
    ├── EmptyChatState.vue       ← stato vuoto (nessuna chat selezionata)
    └── MessagesLoadingState.vue ← spinner caricamento messaggi
```

### La differenza tra View e Component

- **View** = una pagina intera, montata dal router. Ce ne sono solo due: `LoginView` e `HomeView`.
- **Component** = un pezzo riutilizzabile di UI, non ha una route propria. `MessageBubble` per esempio viene usata decine di volte (una per ogni messaggio).

---

## Vue 3 Composition API

Abbiamo usato la **Composition API** con `<script setup>`, la modalità moderna di Vue 3. Invece di organizzare il codice per opzioni (`data`, `methods`, `computed`), si scrive codice JavaScript normale usando le funzioni di composizione di Vue.

Le principali funzioni usate:

```javascript
import { ref, reactive, computed, watch, onMounted, onUnmounted } from 'vue'

const count = ref(0)           // variabile reattiva primitiva (acceduta come count.value)
const obj = reactive({})       // oggetto reattivo (acceduto direttamente come obj.key)
const doubled = computed(() => count.value * 2)  // valore derivato, si aggiorna automaticamente
watch(count, (newVal) => { })  // esegue codice quando count cambia
onMounted(() => { })           // eseguito quando il componente viene montato nel DOM
onUnmounted(() => { })         // cleanup quando il componente viene smontato
```

---

## Gestione dello stato senza Pinia

Non abbiamo usato Pinia (la libreria ufficiale per lo stato globale in Vue 3). Invece abbiamo uno **stato reattivo condiviso** in `services/state.js`:

```javascript
import { reactive } from 'vue'

export const state = reactive({
  userId: null,
  userName: null,
  profilePictureUrl: localStorage.getItem('profilePictureUrl') || null,
})
```

`reactive({})` crea un oggetto dove Vue traccia automaticamente le dipendenze: qualsiasi componente che legge `state.userId` si aggiornerà automaticamente quando `state.userId` cambia.

**Come funziona il login:** `LoginView.vue` chiama `POST /session`, riceve `identifier`, e scrive `state.userId = identifier`. Tutti i componenti che leggono `state.userId` si aggiornano immediatamente — incluso il router guard che reindirizza alla home.

**Persistenza:** `profilePictureUrl` viene salvata nel `localStorage` perché sopravvive al refresh della pagina. `userId` invece non viene persistito: se l'utente fa refresh deve ri-fare il login (comportamento scelto per semplicità).

---

## Il router e i guard di navigazione

In `router/index.js`:

```javascript
router.beforeEach((to) => {
  if (!state.userId && to.path !== '/login') {
    return '/login'   // non autenticato → vai al login
  }
  if (state.userId && to.path === '/login') {
    return '/'        // già autenticato → vai alla home
  }
  return true         // lascia passare
})
```

`beforeEach` è un **guard di navigazione**: viene eseguito prima di ogni cambio di route. Implementa la protezione delle route senza nessuna libreria extra.

---

## Axios: la configurazione centralizzata

In `services/axios.js` creiamo un'istanza axios configurata una volta sola:

```javascript
const api = axios.create({
  baseURL: resolveApiBaseUrl(), // vedi sotto
})

api.interceptors.request.use((config) => {
  if (state.userId) {
    config.headers.Authorization = `Bearer ${state.userId}`
  }
  return config
})
```

L'**interceptor** aggiunge automaticamente l'header `Authorization` a *ogni* richiesta. Non devi ricordarti di aggiungerlo manualmente ogni volta che fai una chiamata API.

**Come viene determinato il `baseURL`?** La funzione `resolveApiBaseUrl()` guarda:
1. Prima la variabile `__API_URL__` (iniettata da Vite al momento della build, da `VITE_API_URL`)
2. Se è vuota, usa `window.location.protocol + '//' + window.location.host`

Questo significa che in Docker (dove nginx fa da reverse proxy sulla stessa porta), il frontend chiama semplicemente la stessa origine e nginx smista le richieste al backend.

---

## Flusso completo: "L'utente invia un messaggio"

Tracciamo esattamente cosa succede dal click al rendering.

**1. Click sul pulsante "Send"** (in `HomeView.vue`)
Il template chiama la funzione `sendMessage()`.

**2. `sendMessage()` in HomeView**
```javascript
async function sendMessage() {
  const text = newMessageText.value.trim()
  // ... validazione locale (testo non vuoto, max 150 chars)

  // Se c'è un'immagine, prima la carica
  if (selectedMediaFile.value) {
    const formData = new FormData()
    formData.append('file', selectedMediaFile.value)
    const uploadResponse = await axios.post('/media', formData, { ... })
    mediaPayload = { url: uploadResponse.data.url, ... }
  }

  // Poi invia il messaggio
  await axios.post(`/conversations/${selectedConversationId.value}/messages`, {
    text: text,
    media: mediaPayload,       // null se solo testo
    replyToId: messageToReply.value?.messageId,  // se è una risposta
  })

  newMessageText.value = ''    // svuota il campo input
  clearSelectedMedia()         // rimuove l'anteprima del file
  messageToReply.value = null  // cancella il contesto di risposta

  // Ricarica i messaggi per mostrare quello appena inviato
  await loadMessages(selectedConversationId.value, { forceScroll: true })
}
```

**3. `loadMessages()` fa `GET /conversations/{id}/messages`**
La risposta JSON viene salvata in:
```javascript
currentMessages.value = data.messages  // array reattivo
```

**4. Vue ri-renderizza automaticamente**
Il template ha `v-for="item in messageTimeline"` dove `messageTimeline` è un `computed` che deriva da `currentMessages`. Quando `currentMessages` cambia, Vue ricalcola `messageTimeline` e aggiorna il DOM. Nessun `document.createElement` manuale.

**5. Lo scroll va in fondo**
```javascript
await scrollToBottom()  // messagesContainer.value.scrollTo({ top: scrollHeight })
```

**6. I messaggi vengono marcati come letti**
Subito dopo il caricamento, `markUnreadMessagesAsSeen()` chiama `PUT /conversations/{id}/messages/{id}/seen` per ogni messaggio non letto non tuo.

---

## Il polling: come riceviamo i messaggi in tempo reale

Non usiamo WebSocket. Ogni 3 secondi, un `setInterval` esegue:

```javascript
pollingInterval = setInterval(async () => {
  await loadConversations()     // aggiorna la lista chat (badge non letti, anteprima)
  if (selectedConversationId.value) {
    await syncData()            // controlla se ci sono nuovi messaggi nella chat aperta
  }
}, 3000)
```

`syncData()` è intelligente: confronta i messaggi già in memoria con quelli appena scaricati e aggiunge solo quelli nuovi (senza far flickerare tutta la lista). Il polling viene pulito in `onUnmounted` per evitare memory leak:

```javascript
onUnmounted(() => {
  if (pollingInterval) clearInterval(pollingInterval)
})
```

---

## Come è integrato Bootstrap

Bootstrap è installato come pacchetto npm (`"bootstrap": "^5.3.3"`). In `main.js`:
```javascript
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.bundle.min.js'
```

Usiamo Bootstrap in due modi:
1. **CSS utility classes** nel template: `class="d-flex gap-2 p-3 rounded-4 bg-primary text-white"` — non scriviamo quasi nessun CSS custom.
2. **Componenti JS di Bootstrap** (modale, dropdown): attivati tramite attributi `data-bs-toggle="modal"` e `data-bs-target="#forwardModal"` nel template. Per chiudere il modale da JavaScript chiamiamo `document.getElementById('closeForwardModalBtn')?.click()`.

---

## Possibili domande d'esame

**D: Perché avete usato la Composition API invece della Options API?**
R: La Composition API permette di raggruppare la logica per **funzionalità** invece che per tipo di opzione. Tutta la logica delle reazioni (state, watcher, funzioni) sta insieme, invece di essere sparsa tra `data`, `methods` e `computed`. Per componenti grandi come `HomeView.vue` è molto più leggibile e manutenibile.

**D: Come funziona la reattività di Vue? Perché il DOM si aggiorna da solo?**
R: Vue avvolge le variabili `ref` e `reactive` in dei Proxy JavaScript. Quando un componente legge una variabile reattiva durante il render, Vue registra quella dipendenza. Quando la variabile cambia, Vue sa esattamente quali componenti devono essere ri-renderizzati e lo fa automaticamente, senza che tu chiami nessuna funzione di "update".

**D: Perché non avete usato Pinia per lo stato globale?**
R: Perché lo stato globale che condividiamo tra componenti è minimo: solo `userId`, `userName` e `profilePictureUrl`. Un oggetto `reactive` esportato è sufficiente e non introduce dipendenze extra. Pinia sarebbe giustificato con stati più complessi, moduli separati e la necessità di DevTools dedicati.
