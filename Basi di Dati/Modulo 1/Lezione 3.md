**reminder: Relazione ha 3 significati**
1) **punto di vista matematico: grado della relazione di domini (prodotto cartesiano dei valori dei domini)**
2) **schema relazionale: a come è fatta la tabella**
3) **associazione tra entità**
# Unione
Consente di costruire una relazione contenente tutte le ennuple che appartengono ad almeno uno dei due operandi.
L'operazione può essere effettuata solo su operandi union compatibili cioè tali che:
- hanno le stesso numero di attributi
- gli attributi corrispondenti devono essere definiti nello stesso dominio
*attenzione*: il SQL il risultato della query non segue il sistema insiemistico
Quando abbiamo problemi di compatibilità prima di fare union possiamo usare le proiezioni.
# Differenza
Si applica a operandi union compatibili, consente di costruire una relazione contenente tutte le tuple che appartengono al primo operando ma non al secondo operando. Non è un'operazione commuttativa. Valgono le stesse considerazioni dell'unione per relazioni che non sono union compatibili.
# Intersezione
Si applica a operandi di union compatibili, e restituisce l'intersezione.
# Prodotto cartesiano
Consente di costruire una relazione contenente tutte le ennuple che si ottengono concatenando un ennupla del primo operando e una ennupla del secondo operando.
# Join naturale
Consente di selezionare le tuple del prodotto cartesiano che soddisfano una funzione composta. Elimina automaticamente i duplicati. Se non c'è alcun elemento con lo stesso valore restituisce un'istanza vuota, mentre se non c'è alcun nome degli attributi in comune restituisce un prodotto cartesiano normale.
Ovviamente poiché il join abbia senso gli attributi con lo stesso nome devono avere anche lo stesso significato.