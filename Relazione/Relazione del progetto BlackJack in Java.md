>[!note] Info.
>Riccardo Lupo
>2136445
>Canale M-Z

_Introduzione_
Vorrei iniziare dicendo che questo progetto è stata un'esperienza particolarmente significativa per me. In un periodo della mia vita in cui sto affrontando molte difficoltà, la programmazione è stata sia una sfida che una sorta di via di fuga, un modo per distrarmi e concentrarmi su qualcosa di costruttivo. Nonostante le difficoltà, sono molto soddisfatto del risultato ottenuto. Voglio anche esprimere la mia gratitudine più sincera alla mia famiglia, che mi ha supportato in ogni momento di questo percorso.

## Capitolo 1: estetica e concept
Per quanto riguarda le carte del gioco, sia il back che il front, sono le tipiche carte da gioco; mentre gli avatar che ho inserito all'interno del gioco sono delle pixelart di alcuni personaggi del mio anime preferito: Neon Genesis Evangelion. 
![[Pasted image 20250201201901.png|300]]
Ho volutamente messo i protagonisti come personaggi giocabili dall'utente mentre gli avatar riservati al dealer e ai bot sono degli "angeli", ovvero gli antagonisti della serie animata. 
![[Pasted image 20250201202215.png|100]]
Ho voluto quindi creare un BlackJack ispirato alla serie (più che un gioco d'azzardo è una sfida per sconfiggere  gli angeli). Motivo per cui come tracce audio del gioco ho inserito la versione 8-bit dei seguenti brani:
- **Fly Me To The Moon** - per quando si gioca
- **The Cruel Angel's Thesis**-per la vittoria  
- **Komm, Susser Tod** - per la sconfitta ed il pareggio
![[Pasted image 20250201201527.png|400]]
E invece la musica del menù? Non è collegata ad Evangelion ma è un omaggio a Sonic, infatti è la storica *OST di Green Hill Zone.*
![[Pasted image 20250201203014.png|400]]

## Capitolo 2: MVC
L' MVC è il design pattern che separa le responsabilità e i compiti in:
- *Model*: si occupa della logica del gioco, come ad esempio il mazzo, i giocatori, la musica,ecc...
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
>- *GameWindow*: inizializza la finestra del gioco e crea il JPanel deck che racchiude a sua volta all'interno tutte le schermate del gioco. Per passare da una schermata all'altra utilizza la classe *Navigator* che implementa observable in modo tale da notificare ogni cambiamento di schermata.
>- *StartPanel, ProfileSelectionPanel, PlayPanel, TiePanel, WinPanel, LosePanel*: sono tutte le schermate del gioco e in base al tipo di schermata disegnano a schermo elementi diversi: ad esempio se ci troviamo nello **StartPanel** verranno disegnate a schermo alcune immagini come il mio logo, il titolo del gioco e verranno aggiunti dei pulsanti per decidere di passare alla selezione del profilo oppure uscire dal gioco.

## Capitolo 3: I Design Pattern
A parte il ben noto MVC ci sono altri design pattern che ho utilizzato all'interno del mio gioco:
- **Observer/Observable:** come da richiesta, ma anche per una corretta implementazione dell'MVC, ho implementato nel codice questo design pattern
- Singleton:
- 