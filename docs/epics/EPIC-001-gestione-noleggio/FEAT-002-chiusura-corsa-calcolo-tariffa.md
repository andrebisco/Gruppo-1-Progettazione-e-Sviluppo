# FEAT-002: Chiusura Corsa e Calcolo Tariffa

| Campo | Specifica |
| :--- | :--- |
| **ID** | FEAT-002 |
| **Titolo** | Chiusura Corsa e Calcolo Tariffa |
| **Parent Epic** | EPIC-001 Gestione Noleggio e Flusso Corsa Veicoli |
| **Owner / Lead** | Tech Lead |
| **Stato** | In Refinement |
| **Target Release** | MVP 1.0 |
| **Priorità** | Must Have |

---

### 1. Descrizione e Valore Utente
* **Descrizione Funzionale:** Consente all'utente di terminare la sessione di noleggio una volta parcheggiato il veicolo, inviando il comando di blocco porte/lucchetto, calcolando la tariffa consuntiva e addebitando l'importo finale.
* **Bisogno Utente / Pain Point:** Garantisce trasparenza e immediatezza sul costo finale sostenuto per il tragitto e assicura che il mezzo sia messo in sicurezza al termine del viaggio.

---

### 2. Regole di Business e Requisiti Funzionali
1. Il termine della corsa è consentito solo se il veicolo si trova all'interno delle aree geografiche operative e non in una "No Parking Zone".
2. Il calcolo della tariffa prende in considerazione i minuti effettivi trascorsi e gli eventuali chilometri extra oltre la soglia base inclusa.
3. All'invio della chiusura, il sistema invia il comando IoT di blocco; solo alla conferma di chiusura fisica ricevuta dalla centralina la corsa si considera conclusa.

---

### 3. Requisiti Non Funzionali (FURPS+)
* **Performance:** Tempo di risposta end-to-end della chiusura e calcolo tariffario < 2 secondi.
* **Security:** Transazione di addebito conforme alle normative PSD2 / Strong Customer Authentication (SCA).
* **Usability:** Ricevuta digitale e riepilogo corsa (mappa percorso, durata, costo) mostrata a schermo e inviata via email.

---

### 4. Decomposizione in User Stories
Elenco delle User Stories atomiche che realizzano la Feature:

| User Story ID | Titolo Story | Punti (SP) | Stato |
| :--- | :--- | :--- | :--- |
| `US-020` | Verifica Area Parcheggio e Comando Blocco | 3 | In Refinement |
| `US-021` | Calcolo Consuntivo Tariffa e Addebito Finale | 3 | In Refinement |

---

### 5. Criteri di Accettazione della Feature (Feature Acceptance Criteria)
- [ ] Il flusso nominale (Happy Path) è completabile dall'interfaccia client.
- [ ] I casi limite ed eccezioni (disconnessione, veicolo non raggiungibile) sono gestiti con feedback chiaro.
- [ ] La feature è integrata e validata nell'ambiente di collaudo con esito positivo dei test di integrazione.
