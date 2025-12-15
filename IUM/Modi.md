### Terminologia
**content**: l'insieme di informazioni che risiedono in un sistema e che hanno significato e utilità per l'utente
**GID (Graphical Input Device)**: meccanismo per comunicare al sistema una particolare locazione o la scelta di un oggetto (tipicamente la posizione del cursore)
**GID button**: bottone principale del GID
**tap**: l'azione di premere e rilasciare un tasto (che automaticamente ritorna nel suo stato originale)
**click**: posizionare il GID e fare un tap sul GID button
**double-click**: posizionare il GID e fare due click di seguito senza spostare il GID tra i due click
**drag, swipe**: premere il GID button, senza rilasciarlo muovere il GID, e poi rilasciarlo (in un'altra locazione)

## Gesture (gesto)
Una sequenza di azioni completata "automaticamente" una volta avviata

>[!example] Example: scrivere una parola comune es: "che"

>[!example] Example: premere il tasto "invio"

>[!example] Example: drag and drop su smartphone:
>- Appoggio il dito su un oggetto, tengo fermo il dito (l'oggetto viene "agganciato")
>- Sposto il dito
>- Stacco il dito dallo schermo
## Modi
I modi si manifestano nella maniera in cui un'interfaccia risponde ai gesti. Dato un gesto, un'interfaccia è in un modo se l'interpretazione di quel gesto è sempre la stessa.
Quando il gesto viene interpretato in maniera diversa, l'interfaccia si trova in un modo diverso.

>[!example] Example: il tasto invio può essere interpretato come "andare a capo" o  "confermare l'inserimento" o "seleziona elemento" (di una select)

>[!warning] oss: Problema dei modi
>*Torcia*
>Una torcia che si accende e spegne facendo il tap su un pulsante.
>*Se ho la torcia in tasca posso dire che succederà se premo il pulsante?*
>L'interfaccia dell'esempio presenta due modi (torcia accesa vs torcia spenta):
>- non permette di stabilire quale operazione si debba effettuare per raggiungere un dato risultato solamente ispezionando il meccanismo di controllo (cioè il pulsante)
>- è necessario verificare anche lo stato del sistema
>
>*Sveglia*
>Bottone per attivare o disattivare una sveglia tradizionale (non su smartphone!):
>- se la sveglia è attiva, premendo il bottone la si attiva
>- se la sveglia è disattivata, premendo il bottone la si attiva
>Al buio non si vede il display: non conoscendo lo stato del sistema, non si può stabilire l'effetto della pressione del bottone

### Luogo dell'attenzione
**DEF:** Oggetto fisico o idea della quale stiamo pensando attivamente e intenzionalmente
*oss:* può esserci solo un luogo dell'attenzione alla volta
*Quali sono le implicazioni?*
*Se qualcosa accade al di fuori del luogo dell'attenzione che succede?*
(concetto collegato a, ma diverso da, *focus*)

>[!example] Example: Caps Lock
>Il tasto blocco maiuscole crea un modo.
>Spesso si inizia a scrivere e ci si accorge dell'errore solo dopo aver digitato alcune parole.
>Eppure:
>- un LED verde sul tasto indica chiaramente lo stato del sistema
>- alcune applicazioni hanno un indicatore di caps lock nella barra di stato
>
>*Allora perché si commette questo errore?*
>*Si può prevenire?*

#### Utente esperto e principiante
I modi possono comunque essere utili, aggiungendo flessibilità, ma possono indurre in errore.
L'esperienza non protegge dagli errori dovuti ai modi: l'esperto ha acquisito delle abitudini, ma anche l'inesperienza non protegge.
#### Minimizzare i "mode errors"
**Mode errors**: mistakes that occur when a user misclassifies or when the user makes an erroneous analysis of a situation
1. Non avere modi
2. Essere sicuri che i modi siano distinti 

