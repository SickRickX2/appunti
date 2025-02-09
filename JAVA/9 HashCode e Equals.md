I metodi *equals()* e *hashcode()* sono metodi importanti in java che ogni oggetto eredita dalla classe Object

## Equals
Il metodo *equals()* viene utilizzato per verificare se due oggetti sono uguali:
>[!tip] Implementazione di base in Object
>Nella sua implementazione  di base in Object il metodo controlla se i due oggetti si riferiscono alla stessa area di memoria ovvero se sono lo stesso oggetto

### Override
Se *equals* viene sovrascritto allora dobbiamo ri-implementare anche *hashCode()*.

Per sovrascrivere *equals()* in modo tale che due oggetti siano logicamente uguali bisogna:
1) **Verificare se l'oggetto è null**: il primo passo è verificare se l'oggetto passato come parametro è null. Se null restituisce false
2) **Verificare se l'oggetto è dello stesso tipo**: il secondo passo è verificare se l'oggetto passato come parametro  è dello stesso tipo della classe in cui  si sta scrivend
