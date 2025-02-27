Una stream in java può essere vista come una sequenza di dati proveniente da una sorgente (ad esempio una collezione o un a array), su cui possiamo effettuare delle operazioni.

Si possono effettuare due tipi di operazioni sulle stream:
- **Operazioni intermedie** che restituiscono una altra stream su cui è possibile effettuare altre operazioni ad esempio: *map(), filter(), sorted()*
- **Operazioni terminali** che restituiscono un tipo atteso e terminano lo stream impedendone il riutilizzo, ad esempio: *collect(), sorted()*

C'è un'altra divisione da fare nelle operazioni:
- **Operazioni Stateless** che vengono elaborate in maniera indipendenete tra gli elementi, il che le rende parallelizabbili come ad esempio: *filter()*
- **Operazioni Statefull** in cui invece l'elaborazione di  un elemento potrebbe dipendere da un altro, questo le rende non parallelizabili ad esempio: *sorted()*

>[!warning] Lazy Behaviour
>Le operazioni intermedie non vengono effettuate subito ma solo al momento dell'esecuzione di un'operazione terminale, questo comportamento serve per ottimizzare il consumo di memoria e ottimizzare le prestazioni

## Tipologie di Stream
### Stream Sequenziali vs Stream Parallele
Una **stream sequenziale** ha un unico elemento corrente, elaborato in modo indipendente dagli altri, una **stream parallela** invece è in grado di suddividere il suo lavoro in più parti, elaborando più elementi contemporaneamente.

## Stream Primitive
Le stream solitamente lavorano solo su degli oggetti, motivo per cui sonon state create delle stream speciali che lavorano solamente sui primitivi, in modo tale che non si debba passare attraverso a delle classi wrapper.
Fanno parte di questa categoria ad esempio: *IntStream, DoubleStream e LongStream*

## Creazione di una Stream
Per creare una stream ci sono diversi modi:
1. Utilizzare *Stream.of(elenco di dati)*
2. Utilizzare *Array.stream(array)*
3. Utilizzare *stream()* o *parallelStream()* delle collection

