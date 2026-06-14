# Guida all'Orale – Docker e Infrastruttura

## Perché Docker?

Docker risolve il classico problema "sul mio computer funziona". Invece di installare Go, Node.js, nginx e configurarli correttamente su ogni macchina, impacchettiamo tutto in **container**: ambienti isolati e autocontenuti che girano in modo identico ovunque.

Un container non è una macchina virtuale completa: condivide il kernel del sistema operativo host ma ha il suo filesystem, le sue dipendenze e il suo processo isolato. È molto più leggero.

---

## I due container: architettura del sistema

```
Host machine
├── Container: wasa-backend  (porta 3000)
│   └── /app/webapi  ← eseguibile Go compilato
│   └── /app/images/ ← file media caricati
│
└── Container: wasa-frontend (porta 80 → esposta su host come 8080)
    ├── nginx             ← web server
    ├── /usr/share/nginx/html/ ← la build Vue (file statici)
    └── nginx.conf        ← configurazione del reverse proxy
```

Tutto è definito in `docker-compose.yml`:

```yaml
services:
  backend:
    build: { dockerfile: Dockerfile.backend }
    ports:
      - "3000:3000"   # host:container

  frontend:
    build: { dockerfile: Dockerfile.frontend }
    ports:
      - "8080:80"     # host porta 8080 → container porta 80
    depends_on:
      - backend       # aspetta che il backend parta prima
```

`depends_on` garantisce l'ordine di avvio, ma non garantisce che il backend sia *pronto* — solo che il container sia *partito*. Per una garanzia più robusta servirebbe un health check, ma per questo progetto è sufficiente.

---

## `Dockerfile.backend` – la build Go

```dockerfile
FROM golang:1.25.1 AS builder     # immagine con tutto il toolchain Go
WORKDIR /src/
COPY . .                           # copia tutto il codice sorgente
RUN go build -o /app/webapi ./cmd/webapi  # compila: produce un singolo eseguibile

FROM debian:bookworm               # immagine finale, molto più leggera
EXPOSE 3000
WORKDIR /app/
RUN mkdir -p /app/images           # directory per i file media caricati
COPY --from=builder /app/webapi ./ # copia SOLO l'eseguibile dalla fase builder
CMD ["/app/webapi"]                # avvia il server
```

Questo è un pattern chiamato **multi-stage build**: usiamo due immagini `FROM`.

- **Fase 1 (`builder`)**: usa l'immagine completa di Go (~800MB) per compilare. Il risultato è un singolo file binario `/app/webapi`.
- **Fase 2 (finale)**: usa Debian minimale (~100MB) e copia solo l'eseguibile compilato. L'immagine finale non contiene il compilatore Go, il codice sorgente, i moduli, niente — solo il binario necessario per girare.

**Perché questa separazione?** L'immagine finale è molto più piccola (risparmio di banda, tempo di avvio più veloce, superficie di attacco ridotta).

---

## `Dockerfile.frontend` – la build Vue

```dockerfile
FROM node:lts AS builder
WORKDIR /app
COPY ./webui/package*.json ./
RUN npm ci                         # installa dipendenze (node_modules)
COPY ./webui .
ARG VITE_API_URL=""                # argomento passabile al build
RUN VITE_API_URL=$VITE_API_URL npm run build  # produce /app/dist/

FROM nginx:stable                  # server web per servire file statici
COPY --from=builder /app/dist /usr/share/nginx/html  # copia la build Vue
COPY nginx.conf /etc/nginx/conf.d/default.conf       # nostra configurazione
```

Anche qui multi-stage:
- **Fase 1**: Node.js compila Vue con Vite. `npm run build` produce una cartella `dist/` con file HTML, CSS e JavaScript ottimizzati. L'intera app Vue diventa file statici.
- **Fase 2**: nginx, che non sa nulla di Node.js, serve quei file statici come se fossero una qualsiasi pagina web.

**L'argomento `VITE_API_URL`** è cruciale. A build time, Vite sostituisce tutte le occorrenze di `__API_URL__` nel codice con il valore di questa variabile. Se lasciata vuota (come in Docker), il frontend usa la stessa origine da cui è servito — e nginx smista le chiamate API al backend.

---

## nginx.conf – il reverse proxy (il pezzo più importante)

```nginx
server {
    listen 80;
    server_name _;

    # Regola 1: le richieste API vanno al backend
    location ~ ^/(session|users|conversations|groups|media|liveness|images) {
        proxy_pass http://backend:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    # Regola 2: tutto il resto è la Single Page Application Vue
    location / {
        root /usr/share/nginx/html;
        try_files $uri $uri/ /index.html;
    }
}
```

### Regola 1: il reverse proxy

Quando il browser fa `GET /conversations/conv_123/messages`, la richiesta arriva a nginx sulla porta 80. nginx controlla: il path inizia con `/conversations`? Sì → `proxy_pass http://backend:3000`. La richiesta viene inoltrata al container backend. La risposta torna al browser come se fosse venuta da nginx stesso.

`http://backend:3000` funziona perché Docker Compose crea una rete interna dove i container si raggiungono per nome (`backend` è il nome del servizio nel compose).

Questo è il **pattern del reverse proxy**: il browser non sa nemmeno che esiste un backend separato. Vede solo nginx sulla porta 8080. Risolve anche il problema del CORS: browser e API sono sulla stessa origine (stesso host, stessa porta), quindi il browser non blocca nulla.

### Regola 2: `try_files` per la Single Page Application

```nginx
try_files $uri $uri/ /index.html;
```

Questa riga è fondamentale per le SPA. Ecco il problema che risolve:

L'utente è sulla pagina `http://localhost:8080/` e naviga all'interno dell'app Vue. Il router Vue cambia l'URL del browser in `http://localhost:8080/` (non ci sono altre route nell'app) — ma questo è gestito da Vue lato client.

Il problema nasce se l'utente **fa refresh** sulla pagina. Il browser fa `GET /` a nginx. nginx cerca un file chiamato `/` nella cartella `html/` — non esiste. Senza `try_files`, risponderebbe 404.

`try_files $uri $uri/ /index.html` dice a nginx: "cerca prima il file esatto, poi una cartella con quel nome, e se non trovi niente servi sempre `index.html`". Nginx restituisce `index.html`, Vue si avvia, il router legge l'URL corrente e porta l'utente nella view giusta. Il refresh funziona.

---

## Il flusso completo di una richiesta in produzione Docker

```
Browser (localhost:8080)
  │
  │  GET /conversations/conv_123/messages
  ▼
nginx (container frontend, porta 80)
  │  → path inizia con /conversations? SÌ
  │
  │  proxy_pass http://backend:3000
  ▼
Go webapi (container backend, porta 3000)
  │  → autentica, interroga SQLite, crea risposta JSON
  ▼
nginx
  ▼
Browser (riceve il JSON)
  │
  └─ Vue aggiorna il DOM con i messaggi
```

---

## Possibili domande d'esame

**D: Cos'è Docker e perché lo usiamo?**
R: Docker è una piattaforma di containerizzazione. Ogni container è un ambiente isolato con le proprie dipendenze, che gira in modo identico su qualsiasi macchina. Lo usiamo per eliminare i problemi di configurazione dell'ambiente, facilitare il deployment e isolare backend e frontend in processi separati con responsabilità distinte.

**D: Cos'è un reverse proxy e perché nginx fa questo ruolo?**
R: Un reverse proxy è un server che riceve le richieste del client e le smista ad altri server interni. Nel nostro caso, nginx riceve tutte le richieste sulla porta 8080, serve i file statici Vue per le richieste "normali" e inoltra le richieste API al container Go sulla porta 3000. Il client vede solo nginx, non sa dell'esistenza del backend. Risolve anche il CORS: browser e backend sono sulla stessa "origine" (8080), quindi non ci sono restrizioni cross-origin.

**D: Perché usi il multi-stage build nei Dockerfile?**
R: Per separare l'ambiente di build dall'ambiente di runtime. L'immagine Go include tutto il toolchain del compilatore (~800MB) ma l'eseguibile finale è un singolo file binario che gira su Debian base (~100MB). Il multi-stage build produce un'immagine finale molto più piccola, più sicura (meno superficie di attacco) e più veloce da scaricare.

**D: Cosa fa esattamente `try_files $uri $uri/ /index.html` in nginx?**
R: Gestisce il refresh nelle Single Page Application. Quando un utente fa refresh su qualsiasi pagina dell'app, il browser chiede quel path a nginx. nginx non trova file corrispondenti (perché la navigazione è gestita da Vue lato client, non da file separati sul server). Invece di rispondere 404, nginx serve sempre `index.html`, che carica Vue, che a sua volta legge l'URL e mostra la pagina corretta. Senza questa direttiva, ogni refresh risulterebbe in un errore 404.

**D: Come comunicano i due container? Come fa nginx a sapere dov'è il backend?**
R: Docker Compose crea automaticamente una rete privata tra i container definiti nello stesso file compose. Ogni container è raggiungibile usando il suo nome di servizio come hostname. Nell'`nginx.conf` scriviamo `proxy_pass http://backend:3000` dove `backend` è esattamente il nome del servizio definito nel `docker-compose.yml`. Docker risolve automaticamente `backend` all'indirizzo IP interno del container.
