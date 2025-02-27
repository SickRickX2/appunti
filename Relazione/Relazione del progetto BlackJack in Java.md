>[!note] Info.
>Riccardo Lupo
>2136445
>Canale M-Z
## Capitolo 1: estetica e concept
Per quanto riguarda le carte del gioco, sia il back che il front, sono le tipiche carte da gioco; mentre gli avatar che ho inserito all'interno del gioco sono delle pixelart di alcuni personaggi del mio anime preferito: Neon Genesis Evangelion. 
![[Pasted image 20250201201901.png|300]]
Ho volutamente messo i protagonisti come personaggi giocabili dall'utente, mentre gli avatar riservati al dealer e ai bot sono degli "angeli", ovvero gli antagonisti della serie animata. 
![[Pasted image 20250201202215.png|100]]
Ho voluto quindi creare un BlackJack ispirato alla serie (più che un gioco d'azzardo è una sfida per sconfiggere  gli angeli). Motivo per cui come tracce audio del gioco ho inserito la versione 8-bit dei seguenti brani:
- **Fly Me To The Moon** - per quando si gioca
- **The Cruel Angel's Thesis**-per la vittoria  
- **Komm, Susser Tod** - per la sconfitta ed il pareggio
![[Pasted image 20250201201527.png|400]]
E invece la musica del menù? Non è collegata ad Evangelion ma è un omaggio a Sonic, infatti è la storica *OST di Green Hill Zone.*
![[Pasted image 20250201203014.png|400]]

## Capitolo 2: Il Gioco
L'utente deve per prima cosa scegliere il profilo da usare per la partita e, contemporaneamente, scegliere anche il numero di bot che giocheranno con lui al tavolo (0,1,2). L'obiettivo del gioco, come nel blackjack reale, è quello di battere il Dealer. 
## Capitolo 3: MVC
L' MVC è il design pattern che separa le responsabilità e i compiti in:
- *Model*: si occupa della logica del gioco, come ad esempio il mazzo, i giocatori, i profili, la musica,ecc...
- *View*: si occupa dell'aspetto grafico
- *Controller*: si occupa di inizializzare il gioco, aggiornare la view, e a coordinare l'interazione tra il model e la view.
L'implementazione dell'MVC permette di estendere il gioco o di fare manutenzione al codice in maniera più semplice.

Nello specifico:

>[!tip] Il Model
>All'interno del model possiamo trovare:
>- *DeckModel, CardModel, Suit, Value*: queste classi si occupano della logica dietro alla creazione delle singole carte che poi verranno usate all'interno del mazzo.
>- *EntityModel, PlayerModel, BotModel,DealerModel*: EntityModel è una classe astratta che rappresenta un giocatore generico che si siede al tavolo del blackjack, essa fornisce proprietà e metodi comuni a tutti i giocatori come ad esempio il pescare le carte della mano, pescare una carta (hit) o rimanere con le carte "originarie" (stay). Infatti le altre classi che estendono EntityModel implementano comportamenti specifici in base al tipo di giocatore, (esempio: il dealer deve necessariamente cercare di battere tutti i giocatori, ma questo non vale per gli altri)
>- *TurnManager*: si occupa della gestione dei turni tra i vari giocatori e notifica gli observers quando si passa da un turno ad un altro ma anche il risultato della partita corrente
>- *AudioManager*: semplicemente gestisce la riproduzione dei brani
>- *ProfileManager, Profile*: si occupa della gestione dei profili, permette di implementarne di nuovi e tiene traccia delle partite giocate e quelle vinte che saranno poi utilizzate nella leaderboard
>- *Leaderboard*: crea e aggiorna la leaderboard usando i dati forniti dal ProfileManager

>[!question] Il Controller
All'interno del controller possiamo trovare:
>- *Game*: inizializza il gioco e crea il gameloop che serve per aggiornare e "ridisegnare" le interfacce ad ogni ciclo
>- *BlackJack*: contiene il main del gioco
>- *PlayPanelController, ProfileSelectionPanelController, StartPanelController*: gestiscono la logica dei pulsanti all'interno delle rispettive schermate e permette l'interazione tra il model e la view in maniera indiretta

>[!Example] La View
>- *GameWindow*: inizializza la finestra del gioco e crea il JPanel deck che racchiude a sua volta all'interno tutte le schermate del gioco. Per passare da una schermata all'altra utilizza *Navigator* che implementa observable in modo tale da notificare ogni cambiamento di schermata.
>- *StartPanel, ProfileSelectionPanel, PlayPanel, TiePanel, WinPanel, LosePanel*: sono tutte le schermate del gioco e in base al tipo di schermata disegnano a schermo elementi diversi: ad esempio se ci troviamo nello **StartPanel** verranno disegnate a schermo alcune immagini come il mio logo, il titolo del gioco e verranno aggiunti dei pulsanti per decidere di passare alla selezione del profilo oppure uscire dal gioco.

## Capitolo 4: Design Pattern
A parte il ben noto MVC ci sono altri design pattern che ho utilizzato all'interno del mio gioco:
- **Observer/Observable:** come da richiesta, ma anche per una corretta implementazione dell'MVC, ho implementato nel codice questo design pattern che serve a notificare il cambiamento di stato di un oggetto (**observable**) agli oggetti osservatori (**observers**) in modo tale che si aggiornino in base alle loro funzionalità.
  1) Nel mio codice un esempio di **Observable** è *Navigator*;  ***navigator*** notifica il frame  *GameWindow* (che implementa **Observer**)  a quale panel bisogna cambiare. In questo modo ho potuto creare un panel denominato ***deck*** che contiene al suo interno tutte le schermate ma vengono mostrate a schermo solamente una alla volta.
```java
public class Navigator extends Observable {  
     public void navigate(Screen screen) {  
        setChanged();  
        notifyObservers(screen);  
    }}
```
e in GameWindow:
```java
@Override  
public void update(Observable o, Object arg) {  
    if (o instanceof Navigator && arg instanceof Screen screen)  
        ((CardLayout) deck.getLayout()).show(deck, screen.name());  
}
```
 2) Un altro utilizzo di Obsever/Observable si può trovare nelle classi *TurnManager* (**Observable**) e *PlayPanel* (**Observer**). Il TurnManager notifica il panel se il giocatore ha vinto, perso o pareggiato in maniera tale che la schermata finale sia coerente con l'esito del gioco.
```java
#In PlayPanel
@Override  
public void update(Observable o, Object arg) {  
    if (arg instanceof String result) {  
        switch (result) {  
            case "WIN":  
                switchToResultPanel(true, false, false);  
                break;  
            case "TIE":  
                switchToResultPanel(false, true, false);  
                break;  
            case "LOSE":  
                switchToResultPanel(false, false, true);  
                break;  
        }    } else {  
        disableButtons();  
    }}
```
- **Singleton**: ho implementato questo design pattern in tutte le classi che devono avere solo un'istanza: i giocatori, i manager e la leaderboard. Il design pattern "singleton" evita la duplicazione o incongruenze nei dati, si usa un costruttore privato in maniera tale che la classe non venga istanziata da altre parti del codice, per accedere all'istanza si usa il metodo  statico *getIstance()*  e nel caso in cui l'istanza non esista (quindi è pari a null) il metodo chiama il costruttore privato per poterla creare.
```java
public class DealerModel {  
    private static DealerModel instance;  
  
    private DealerModel() {}  
  
    public static DealerModel getInstance() {  
        if (instance == null) {  
            instance = new DealerModel();  
        }        return instance;  
    }  
    // altri metodi... 
}
```
## Capitolo 5: Stream
Nel mio programma l'utilizzo delle stream viene impiegato per creare la leaderboard, iterando sui profili e comparando tra loro il proprio numero di vittorie creo una lista ordinata che rappresenta la classifica.
```java
public class Leaderboard {  
    private static Leaderboard instance = null;  
    private List<Profile> profiles;  
  
     private Leaderboard() {  
        ProfileManager profileManager = ProfileManager.getInstance();  
        profiles = IntStream.range(0, profileManager.getProfilesSize())  
                .mapToObj(profileManager::getProfile)  
                .collect(Collectors.toList());  
    }  
 public List<Profile> getTopProfiles(int limit) {  
        return profiles.stream()  
                .sorted((p1, p2) -> Integer.compare(p2.getWins(), p1.getWins()))  
                .limit(limit)  
                .collect(Collectors.toList());  
    }}
```