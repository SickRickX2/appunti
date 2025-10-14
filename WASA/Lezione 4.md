REST è un modo per combinare server e client in maniera standardizzata. Si concentra sullo scambio di risorse e non sull'efficienza.Pensata per sistemi distribuiti.

>[!note] Risorsa
>Qualsiasi cossa che in astrazione ha senso considerare oggetto da manipolare. Una collezione di risorse è una risorsa. 

Noi lavoriamo particolarmente sulla rappresentazione di queste risorse.
Li identifichiamo con gli **identificatori**, *locator (URL)*. Sono stringhe che ci aiutano ad identificare le risorse.
Dobbiamo pensare le risorse come sostantivi e i metodi per manipolarli come i verbi. 

In generale cerchiamo di non mettere le operazione nei locatori, identifichiamo solo le risorse non le azioni su di esse.

>[!note] Vincoli RESTFUL
>- client-server
>- stateless
>- cacheable
>- uniform-interface
>- layered-system




- *client-server* applica separazione delle responsabilità, maggiore scalabilità
- *stateless* ogni richiesta deve contenere tutte le informazioni necessarie per essere compresa, non può sfruttare alcun contesto memorizzato sul server. Lo stato della sessione deve essere mantenuto interamente sul client.