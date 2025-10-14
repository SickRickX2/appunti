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
- *caheable* permettere al client di riutilizzare una rappresentazione della risorsa che è considerata cacheable, il periodo di tempo che una eisorsa può essere messa in cache è specificato nella risposta.
*uniform-interface* un'interfaccia uniforme tra i componenti promuove la standardizzazione. I quattro vincolo dell'interfaccia sono:
	- identificazione delle risorse
	- manipolazione delle risorse tramite rappresentazioni
	- messaggi autodescrittivi
	- hypermedia come motore 
	API REST basate su HTTP usano metodi standard e gli URL per identificare risorse.

 ```YAML
 openapi: 3.0.4
info: 
  title: Hi-lo The Game
  description: |-
    This is a game in which clients can:
    - bet on a number between 1 and 100
    - receive a response from the oracle:
      - hi if the number is too high compared to the game specific secret number
      - lo if it s too low
      -correct if it is the secret number
  version: 0.0.1
paths:
  /games:
    description: this is a test
  /game/{id}:
    description: this is a test
 
 ```
