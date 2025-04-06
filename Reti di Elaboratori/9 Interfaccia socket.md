**Comunicazoine tra processi**
Nel paradigma client/server la *comunicazione* a livello applicazione avviene *tra due programmi applicativi in esecuzione chiamati procesi: un client e un server*.
- Un client è un programma in esecuzione che inizia la comunicazione inviando una richiesta
- Un server è un altro programma applicativo che attende le richieste dai client
### API: Application Programming Interface 
Un linguaggio di programmazione prevede un insieme di istruzioni matematiche, un insieme di istruzioni per la manipolazione delle stringhe, un insieme di istruzioni per la gestione dell'input/output ecc.

Se si vuole sviluppare un programma capace di comunicare con un altro programma, è necessario un **nuovo insieme di istruzioni** per chiedere ai primi quattro livelli dello stack TCP/IP di aprire la connessione, inviare/ricevere dati e chiudere la connessione.

Un insieme di istruzioni di questo tipo viene chiamato **API (Application Programming Interface)**.

>[!note] API di comunicazione
>![[Pasted image 20250405173210.png]]

>[!tip] Comunicazione tra processi: socket
>- Appare come un terminale o un file ma è un'entità fisica
>- Astrazione
>- Struttura dati creata e utilizzata dal programma applicativo
>- Comunicare tra un processo client e un processo server significa comunicare tra due socket create nei due lati di comunicazione.
>
>![[Pasted image 20250405173800.png]]
>![[Pasted image 20250405174312.png]]

### Indirizzamento dei processi 
 Affinché un processo su un host invii un messaggio a un processo su un altro host, il mittente deve identificare il processo desinatario. Un host ha indirizzo IP univoco a 32 bit.
 >[!danger] D: è sufficiente conoscere l'indirizzo IP dell'host su cui è in esecuzione il processo per idetnificare il processo stesso?
 
 >[!tip] Risposta: No, sullo stesso host possono essere in esecuzione molti processi.

L'identificatore comprende sia l'indirizzo IP che i numeri di porta associati al processo in esecuzione su un host.
Esempi di numeri di porta:
- HTTP server: 80
- Mail server: 25

*N.B* Il numero di porta è una delle informazione contenute negli header di livello di trasporto per capire a quale applicazione bisogna.
![[Pasted image 20250405181006.png]]
## Individuare i socket address
L'interazione tra client e server è bidirezionale, è necessaria quindi una coppia di indirizzi socket: *locale* (mittente) e *remoto*(destinatario).
L'indirizzo locale in una direzione è l'indirizzo remoto nell'altra direzione.

>[!note] Individuare i socket lato server
>Il server ha bisogno di un socket address locale(server) e un remoto(client) per comunicare.
>- *Socket address locale*: è fornito dal sistema operativo, conosce l'indirizzo IP del computer su cui il server è in esecuzione. Il numero di porta è noto al server perché assegnato dal progettista (numero well knwon o scelto)
>- *Socket address remoto*: è il socket address locale del client che si connette, poiché numerosi client possono connettersi, il server non può a priori conoscere tutti i socket address, ma li trova all'interno del pacchetto di richiesta

>[!note] Lato client
>Il client ha bisogno di un socket address locale (client) e un remoto (server) per comunicare.
>- *Socket address locale*: fornito dal sistema operativo su cui il client è operativo, il numero di porta è assegnato temporaneamente dal sistema operativo(numero di porta effimero o temporaneo non utilizzato da altri processi)
>- *Socket address remoto*: numero di porta noto in base all'applicazione (http porta 80), IP fornito dal DNS (Domain Name System). Oppure porta e indirizzo noti al programmatore quando si vuole verificare il corretto funzionamento di un'applicazione.

### Utilizzo dei servizi di livello trasporto
Una coppia di processi fornisce servizi agli utenti di Internet, siano questi persone o applicazioni. La coppia di processi, tuttavia, deve utilizzare i servizi offerti dal livello trasporto per la comunicazione poiché non vi è una comunicazione fisica a livello applicazione.

Nel livello trasporto della pila di protocolli TCP/IP sono previsti due protocolli principali:
- Protocollo UDP
- Protocollo TCP
In base alle nostre esigenze di sicurezza, affidabilità, velocità si sceglie a priori il protocollo da usare, in base al quale il servizio di trasposto cambia il tipo di socket da usare.

## Programmazione con socket
L' obiettivo è imparare a costruire un'applicazione client/server che comunica utilizzando le socket.
**Socket API**
Introdotta in UNIX nel 1981, esplicitamente creata, usata, distribuita dalle appplicazioni. Paradigma client/server. 
Offre due tipi di servizio di trasporto tramite una socket API:
- datagramma inaffiidabile
- affidabile, orientata ai byte
>[!note] socket
>Interfaccia di un *host locale*, creata dalle applicazioni, controllata dal SO, in cui il processo di un'applicazione può inviare e ricevere messaggi al/dal processo di un'altra applicazione.

### Programmazione socket con TCP
Il *socket* è un'ingresso tra il processo di un'applicazione e il protocollo di trasporto end-to-end (UDP o TCP).
*Servizio TCP*: trasferimento affidabile di **byte** da un processo all'altro.

**Il client deve contattare il server**
- Il processo server deve essere in corso di esecuzione (sempre attivo). 
- Il server deve aver creato un socket che dà il benvenuto al contatto con il client.
**Il client contatta il server**
- Creando un socket TCP, specificando l'indirizzo IP, il numero di porta del processo server
- Quando il *client crea il socket*: il client TCP stabilisce una connessione con il server TCP
![[Pasted image 20250406172352.png|350]]

Quando viene contattato dal client, il *server TCP crea un nuovo socket* per il processo server per comunicare con il client
- consente al server di comunicare con più client
- numeri di porta di origine usati per distinguere i client
>[!warning] Terminologia
>Un *flusso*(stream) è una sequenza di caratteri che influisce verso/da un processo.
>Un *flusso d'ingresso*(input stream) è collegato a un'origine di input per il processo, ad esempio la tasteria o la socket
>Un *flusso di uscita*(output stream) è collegato a un'uscita per il processo, ad esempio il monitor o la socket.

>[!example] Esempio di applicazione client-server
>1) Il client legge una riga dall'input standard (flusso **inFromUser**) e la invia al server tramite la socket(flusso **outToServer**)
>2) Il server legga la riga dalla socket
>3) Il server converte la riga in lettere maiuscole e la invia al client
>4) Il client legge nella sua socket la riga modificata e la visualizza (flusso **inFromServer**)

**Package java.net**
Il package *java.net* fornisce interfacce e classi per l'implementazione di applicazioni di rete.
- le classi Socket e ServerSocket per le connessioni TCP
- la classe DatagramSocket per le connessioni UDP
- la classe URL per le connessioni HTTP
- la classe InetAddress per rappresentare gli indirizzi Internet
- la classe URLConnection per rappresentare le connessioni a un URL

>[!Example] Client Java (TCP)
>```Java
>import java.io.*
>import java.net.*
>class TCPClient{
>	public static void main(String args[]) throws Exception{
>		String sentence;
>		String modifiedSentence;
>		BufferedReader inFromUser = new BufferedReader(new InputStreamReader(System.in));
>		Socket clientSocket = new Socket("hostname", 6789);
>		DataOutputStream outToServer = new DataOutputStream(clientSocket.getOutputStream());
>		BufferedReader inFromServer = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
>		System.out.print("Inserisci una frase: ");
>		sentence = inFromUser.readLine();
>		outToServer.writeByte(sentence + '\n');
>		modifiedSentence = inFromServer.readLine();
>		System.ot.println("FROM SERVER:" + modifiedSentence);
>		clientSocket.close();
>	}
>}


>```