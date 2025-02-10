L'algoritmo per la cnacellazione del tipo utilizzato dal compilatore per tradurre la classe generica in **bytecode Java**:
1. Elimina la sezione del tipo parametrico e sostituisce il tipo parametrico con quello reale
2. Per default il tipo generico viene sostituito con il tipo Object (a meno di vincoli sul tipo)
3. Viene creata una copia  della classe o metodo

Un generico equivale a un tipo Object su cui non devono essere fatte conversioni o downcasting. Non si possono conoscere il tipo generico a tempo di esecuzione per via della cancellazione del tipo.