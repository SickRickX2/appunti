# Strutture di Controllo del SO
Il SO è l'entità che gestisce l'uso delle risorse di sistema da parte dei processi, in primis il processore. Poichè il SO deve gestire sia i processi che le risorse, deve conoscere lo stato di ogni processo e di ogni risorsa. Per ogni entità da gestirer il SO costruisce e mantiene una o più tabelle.
>[!note] Tabelle di Memoria
>Le tabelle di memoria sono usate per gestire sia la memoria principale che quella secondaria, quest'ultima come vedremo più avanti serve per la memoria virtuale. Devono comprendere le seguenti informazioni:
>- allocazione di memoria principale da parte dei processi
>- allocazione di memoria secondaria da parte dei processi
>- attributi di protezione per l'accesso a zone di memoria condivisa
>- informazioni per gestire la memoria virtuale

>[!note] Tabelle per l'I/O
>Vengono usate dal SO per gestire i dispositivi e i canali di I/O. Devono comprendere le seguenti informazioni:
>- se il dispositivo è disponibile o già assegnato
>- lo stato dell'operazione di I/O
>- la locazione in memoria principale usata come sorgente o destinazione del trasferimento