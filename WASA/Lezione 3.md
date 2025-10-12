# JSON
*JavaScript Object Notation*, formato leggero per lo scambio di dati (dati inviati con richieste e risposte RESTful).
Utilizzato anche per archiviare dati (estensione.json). Formato di testo (basato su un sottoinsieme di Javascript). 
### Oggetti e Array
**object** (oggetto) $\to$ facile da leggere e scrivere per gli umani
**array**(array)$\to$ facile da analizzare e generare per le macchine

>[!note] Oggetto
>**nome**: stringa tra " ", unica all'interno dell'oggetto (a.k.a. "chiave" o "campo")
>**valore**: numero, stringa, booleano, null, array, object

>[!note] Array
>Elenco ordinato di valori separati da virgole, racchiuso tra parentesi quadre

## YAML
*YAML-YAML Ain't Markup Language* 
Linguaggio di serializzazione dei dati pensato per gli umani, per file di configurazione, per archiviare dati o per scambiare dati.
Usa un formato di testo basato sull'indentazione python.
### YAML superset di JSON
I file JSON sono YAML validi.
{} accettati per le mappe (oggetti)
[] accettati per le liste (array)
\# per i commenti
I documenti possono opzionalmente iniziare con --- e finire con ...
Un file può contenere più documenti.

# API
Un'**API (Application Programming Interface)** è la *definizione delle interazioni consentite* tra due parti di un software. L'API funge da contratto, specificando come un pezzo di codcie o un servizio puà interagire con un altro.
### Elementi di un Contratto
L'API definisce in dettaglio il "contratto" di interazione tra il **CONSUMER** (il client) e il **PROVIDER**(il servizio) Essa specifica:
- Le richieste possibili
- I parametri delle richieste
- I valori di ritorno
- Qualsiasi formato di dato richiesto 

**Benefici**
L'adozione di un'API porta vantaggi fondamentali nell'architettura software:
- *Interfaccia Esplicita:* definisce chiaramente le aspettative e le modalità di interazione
- *Contratto Infrangibile:* Stabilisce un insieme di regole che entrambe le partidevono rispettare
- *Information Hiding (Nascondimento delle Informazioni):* La logica interna del Provider (come i dati vengono processati o archiviati ) rimane nascosta al Consumer. Il client deve solo conoscere l'interfaccia.

### API Locali e Remote
Esistono diverse categorie di API in base alla loro posizione e funzione: 
**API Locali**
- API per i linguaggi di programmazione
- API del sistema operativo 
- API delle librerie softwarre 
- API hardware
**API Remote (Web API):**
- Interfacce di programmazione basate su protocolli di rete (tipicamente HTTP), come le API RESTful
La distinzione si basa sull'accessibilità
*API Private*: Destinate all'uso interno di un'azienda o un sistema chiuso. L'accesso è limitato ai componenti interni.
*API Pubbliche*: Disponibili per l'uso da parte del pubblico. L'accesso può essere limitato solo ad alcuni utenti tramite **API Tokens**.

>[!tip] Interfaccia e Stabilità
>**Stabilità dell'interfaccia** i cambiamenti potrebbero rompere la compatibilità con i clienti esistenti.
>**Marcatori di Stato**:
>	- *beta*: Indica che le parti potrebbero cambiare perché non sono ancora stabili
>	- *deprecated:* Indica che le parti verranno rimosse o non saranno più supportate in futuro

### Documentazione e definizione
Per stabilire il contratto, l'API deve essere definita esplicitamente.
La definizione può avvenire attraverso *documentazione* (testo, esempi, manuali). Oppure attraverso un 