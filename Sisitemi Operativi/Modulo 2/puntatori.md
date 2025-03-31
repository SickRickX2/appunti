sono variabili che contengono l'indirizzo di memoria di una locazione di memoria.
Il puntatore punta sempre al primo byte del tipo di dato memorizzato.
- Valore diretto: indirizzo di una cella di memoria
- Valore indiretto: valore contenuto nell'indirizzo di memoria in cui indirizzo è il valore diretto (quello memorizzato nella locazione di memoria)
>[!tip] Aritmetica dei puntatori
>Si possono fare operazioni sugli indirizzi oltre che sui valori a cui puntano.
>```C
>int *ptr;
>ptr = ptr+1; 
>// viene incrementato di 4 locazioni di memoria
>ptr = ptr+n;
>//viene incrementato di 4*n locazioni di memoria
>```

Nel caso di vettori, il puntatore al primo elemento dell'array e puntatore al vettore sono la stessa cosa.
```C
int vect[10];
int *ptr = NULL;
ptr = &vect[10]; // puntatore al primo elemento
ptr = vect; //puntatore al vettore
```
