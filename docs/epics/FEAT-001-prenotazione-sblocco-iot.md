# FEAT-001: Prenotazione e Sblocco IoT Veicolo

| Campo | Specifica |
| :--- | :--- |
| **ID** | FEAT-001 |
| **Titolo** | Prenotazione e Sblocco IoT Veicolo |
| **Parent Epic** | EPIC-001 Gestione Noleggio e Flusso Corsa Veicoli |
| **Owner / Lead** | Tech Lead |
| **Stato** | Ready for Dev |
| **Target Release** | MVP 1.0 |
| **Priorità** | Must Have |

---

### 1. Descrizione e Valore Utente
* **Descrizione Funzionale:** Consente all'utente autenticato di selezionare un veicolo (auto o bici) dalla mappa, richiedere la prenotazione ed inviare il comando di sblocco remoto per avviare il viaggio.
* **Bisogno Utente / Pain Point:** Elimina la necessità di chiavi fisiche o procedure manuali complesse, permettendo un accesso immediato al mezzo prescelto direttamente da smartphone.

---

### 2. Regole di Business e Requisiti Funzionali
1. Un utente può prenotare/sbloccare un solo veicolo alla volta.
2. L'utente deve trovarsi entro un raggio di 50 metri dal veicolo per consentire l'invio del comando di sblocco.
3. In caso di mancata risposta hardware entro 8 secondi, il sistema deve tentare un secondo invio prima di segnalare errore.

---

### 3. Requisiti Non Funzionali (FURPS+)
* **Performance:** Tempo di risposta end-to-end del comando di sblocco < 3 secondi.
* **Security:** Richiesta autenticata con Bearer Token JWT valido e autorizzazione su prenotazione specifica.
* **Usability:** Feedback visivo chiaro di caricamento e animazione di conferma avvenuto sblocco.

---

### 4. Decomposizione in User Stories
Elenco delle User Stories atomiche che realizzano la Feature:

| User Story ID | Titolo Story | Punti (SP) | Stato |
| :--- | :--- | :--- | :--- |
| `US-010` | Avvio Noleggio e Comando Sblocco IoT | 3 | Ready for Dev |
| `US-011` | Gestione Timeout e Feedback Errore Connessione | 2 | Ready for Dev |

---

### 5. Criteri di Accettazione della Feature (Feature Acceptance Criteria)
- [ ] Il flusso nominale (Happy Path) è completabile dall'interfaccia client.
- [ ] I casi limite ed eccezioni (disconnessione, veicolo non raggiungibile) sono gestiti con feedback chiaro.
- [ ] La feature è integrata e validata nell'ambiente di collaudo con esito positivo dei test di integrazione.
