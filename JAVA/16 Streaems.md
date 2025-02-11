Una stream in java puòòò essere vista come una sequenza di dati proveniente da una sorgente (ad esempio una collezione o un a array), su cui possiamo effettuare delle operazioni.

Si possono effettuare due tipi di operazioni sulle stream:
- **Operazioni intermedie** che restituiscono una altra stream su cui è possibile effettuare altre operazioni ad esempio: *map(), filter(), sorted()*
- **Operazioni terminali** che restituiscono un tipo atteso e terminano lo stream impedendone il riutilizzo, ad esempio: *collect(), sorted()*

C'è un'altra divisione da fare nelle operazioni:
- **Oper**