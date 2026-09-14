# US-011: Gestione Timeout e Feedback Errore Connessione

| Campo | Specifica |
| :--- | :--- |
| **ID** | US-011 |
| **Titolo** | Gestione Timeout e Feedback Errore Connessione |
| **Parent Feature** | FEAT-001 Prenotazione e Sblocco IoT Veicolo |
| **Parent Epic** | EPIC-001 Gestione Noleggio e Flusso Corsa Veicoli |
| **Autore (PO / Analyst)** | Federico Chiappa |
| **Assegnatario (Dev)** | Team Dev |
| **Sprint / Iterazione** | Sprint 1 |
| **Stima (Story Points)** | 2 |
| **Stato** | Ready for Dev |

---

### 1. Dichiarazione della Storia (Formulato Connextra)

> **Come** Utente del servizio di noleggio  
> **voglio** ricevere una gestione chiara ed immediata in caso di mancata risposta del veicolo allo sblocco  
> **affinché** io non subisca addebiti indebiti e possa scegliere un veicolo alternativo senza blocchi di sessione.

---

### 2. Checklist di Conformità INVEST

* [x] **I - Independent:** La storia è autosufficiente e rilasciabile autonomamente senza bloccare altre storie.
* [x] **N - Negotiable:** L'implementazione è stata discussa con il team ed è aperta ad aggiustamenti tecnici.
* [x] **V - Valuable:** Produce un valore percepibile per l'utente finale (nessun task puramente tecnico travestito da storia).
* [x] **E - Estimable:** Il team ha compreso il perimetro e ha assegnato una stima condivisa in Story Points.
* [x] **S - Small:** Completabile all'interno di un singolo sprint (1-3 giorni di lavoro effettivo).
* [x] **T - Testable:** I criteri di accettazione consentono un collaudo oggettivo Pass/Fail.

---

### 3. Criteri di Accettazione BDD (Behavior-Driven Development — Gherkin)

#### Scenario 1: Timeout Risposta Centralina IoT (Edge / Error Path)
```gherkin
Scenario: Mancata risposta ACK dalla centralina del veicolo
  Given il comando di sblocco è stato inviato dal backend alla centralina IoT
  And la pre-autorizzazione di 5.00 EUR è stata congelata con successo
  When la centralina IoT non restituisce conferma ACK entro 8 secondi
  Then il sistema effettua un retry automatico del comando
  And se entro ulteriori 5 secondi non giunge risposta, annulla la sessione di noleggio
  And rilascia immediatamente la pre-autorizzazione bancaria di 5.00 EUR
  And mostra un avviso "Veicolo non raggiungibile. Riprova o seleziona un altro mezzo"
```

#### Scenario 2: Segnalazione automatica per manutenzione veicolo (Exception Path)
```gherkin
Scenario: Blocco automatico veicolo dopo fallimenti ripetuti
  Given che il veicolo "CAR-102" ha fallito due tentativi consecutivi di sblocco da parte di utenti diversi
  When la seconda richiesta va in timeout
  Then il sistema imposta automaticamente lo stato del veicolo in "IN_MANUTENZIONE"
  And rimuove il veicolo dai risultati di ricerca della mappa utente
  And genera un alert per la squadra di assistenza operativa
```

---

### 4. Note Tecniche e Dipendenze
* **Endpoint API di Riferimento:** `POST /api/v1/rentals/cancel-timeout` (OpenAPI Spec).
* **Componenti UI / Wireframe:** Toast Error Banner e Modal Selezione Mezzo Alternativo.
* **Vincoli Dati / Entità Coinvolte:** Meccanismo di Retry Broker MQTT, Coda Eventi Dead-Letter Queue (DLQ).

---

### 5. Definizione dei Cancelli di Qualità

#### Definition of Ready (DoR) per questa Storia
- [x] Il ruolo utente e il beneficio di business sono univoci e chiari.
- [x] Almeno 2 scenari BDD Gherkin (Happy Path + eccezione) sono definiti e approvati.
- [x] Le dipendenze API e i wireframe UI sono disponibili e consultabili.
- [x] La storia è stata stimata dal team in Planning Poker.

#### Definition of Done (DoD) per questa Storia
- [ ] Codice scritto, formattato e passato dal linter senza warning.
- [ ] Unit test scritti e superati con coverage >= 80% sulla logica di business.
- [ ] Pull Request revisionata e approvata da almeno un pari (Peer Review).
- [ ] Test di integrazione superati in pipeline CI automatica.
- [ ] Criteri BDD verificati con successo in ambiente di staging.
