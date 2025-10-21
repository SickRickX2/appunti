>[!note] Campi opzionali
>In OpenAPI si dice cosa è required e non cosa è opzionale. Il required è legato alle regole di validazione del payload e non il comportamento logico dell'API. Di questo se ne occupa il backend.

>[!note] URI
>Principio: URI rappresentano Risorse, non Azioni

>[!tip] PUT vs PATCH
>Quando si tratta di modificare una risorsa viene usato patch invece di put (che sostituisce l'intera risorsa)


## API Best Practices
**Design FIrst e Connexion**
Facciamo una connessione tra API e Backend.
Definiamo prima il contratto API in un file YAML e poi implementiamo il backend Pyhton per rispettare tale contratto.
Usiamo il *Connexion(Python)* come il framework che funge da ponte. 
- legge il file YAML
- gestisce il routing automatico
- esegue la validazione automatica del corpo JSON della richiesta contro lo schema definito nello YAML

## Pokémon Team Builder
