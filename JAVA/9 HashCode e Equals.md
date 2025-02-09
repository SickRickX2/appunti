I metodi *equals()* e *hashcode()* sono metodi importanti in java che ogni oggetto eredita dalla classe Object

## Equals
Il metodo *equals()* viene utilizzato per verificare se due oggetti sono uguali:
>[!tip] Implementazione di base in Object
>Nella sua implementazione  di base in Object il metodo controlla se i due oggetti si riferiscono alla stessa area di memoria ovvero se sono lo stesso oggetto

### Override
Se *equals* viene sovrascritto allora dobbiamo ri-implementare anche *hashCode()*.

