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
L'API definisce in dettaglio il "contratto" di interazione tra il **CONSUMER** (il client) e il **PROVIDER**(il servizio)