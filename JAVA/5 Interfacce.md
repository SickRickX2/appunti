Le interfacce sono uno strumento fornito da java per risolver il problema di *ereditarietà multipla*, le classi non possono estendere più di una classe, ma è possibile implementare più di un interfaccia.

Infatti non posssono essere istanziate ed il loro obiettivo è quello di fornire dei metodi che devono essere implementati da una classe concreta (le classi astratte non devono fornire un implementazione dei metodi).

Le interfacce possono contenere:
- **Metodi** senza implementazione che sono implicitamente *abstract* e *public*
- **Campi costanti** che sono implicitamente *public, static, final*
- **Metodi di Default** con implementazione ma che sono implicitamente *public* e *static*
Inoltre un'interfaccia può estendere un altra interfaccia ed ereditare tutti i suoi metodi.
>[!note] ### SAM
>Una SAM è un'interfaccia che contiene un solo metodo astratto, ovvero un metodo che non ha un'implementazione
>>[!warning] Osservazione
>> ogni SAM è anche un'interfaccia funzionale, ma non è detto che  un'interfaccia funzionale sia una SAM

>[!tip] ### Interfacce Funzionali
>Un'interfaccia funzionale è un'interfaccia che contiene





