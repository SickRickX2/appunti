I tipi generici in Java sono un potente meccanismo che permette di scrivere codice flessibile e riutilizzabile; dando la possibilità di definire classi, interfacce e metodi che operano su tipi di dati specificati solo al momento dell'utilizzo.

Ad esempio le collezioni sono classi generiche dove il tipo su cui operano è definito soltanto al mometno dell'istanziamento attraverso l'*operatore diamante* <>. Questo ha permesso di utilizzare un singolo codice per creare delle collection per qualsiasi tipo, ad esempio senza i tipi generici si sarebbe dovuto definire un tipo specifico di ArrayList per ogni tipo d'oggetto esistente.

>[!danger] Implementazione dei Tipi Generici
>I tipi generici sono implementati attraverso la cancellazione del tipo.

## Limiti
>[!note] No Primitivi
>Non è possibile utilizzare i tipi primitivi con tipi generici, questo perché durante la cancellazione del tipo, il tipo generico viene sostituito con Object e i primitivi non possono essere trattati come oggetti.

>[!note] No ereditarietà dei tipi generici
>Per le classi generiche non vale l'ereditarietà dei tipi generici 

>[!note] No upcasting
>Non è permesso l'upcasting nei tipi generici, ad esempio:
>Creiamo una lista di mele
>```java
`ArrayList<Mela> mele = new ArrayList<Mela>();
Definiamo un metodo che prende in input una lista di frutti e inserisce una pera (sotto classe di frutto)

```java
public static void aggiungiPera(`ArrayList<Frutto> frutti) {
   frutti.add(new Pera());
}
```

Ora, proviamo a utilizzare la lista di mele come input del metodo appena citato.

```java
aggiungiPera(mele);
```

Tuttavia, questo ci darà un errore di compilazione. Il motivo è che il metodo `aggiungiPera` prende in input una lista di frutti, mentre noi gli stiamo passando una lista di mele. Questo non è possibile perché non si può fare l'upcasting dei tipi generici.

Se fosse possibile, avremmo come risultato una lista di mele che contiene una pera, il che non è corretto. La lista di mele dovrebbe contenere solo mele, non frutti di tipo diverso.

>[!note] Estendere Classi Generiche
>In java è possibile estendere classi generiche o implementare interfacce generiche con classi a loro volta generiche, è possibile scegliere il tipo nelle loro sotto classi.

È possibile definire metodi generici in classi non generiche.

## Overloading & Overriding Metodi Generici

Un metodo generico può essere sovraccaricato anche da un metodo non generico ma con lo stesso nome e numero di parametri. Quando il compilatore riceve una chiamata a questo metodo cerca prima l'implementazione più specifica, ovvero quella non generica e poi il generico, per garantire un'ottimizzazione in base al tipo.