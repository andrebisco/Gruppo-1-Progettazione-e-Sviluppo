# US-010: Avvio Noleggio e Comando Sblocco IoT

| Campo | Specifica |
| :--- | :--- |
| **ID** | US-010 |
| **Titolo** | Avvio Noleggio e Comando Sblocco IoT |
| **Parent Feature** | FEAT-001 Prenotazione e Sblocco IoT Veicolo |
| **Parent Epic** | EPIC-001 Gestione Noleggio e Flusso Corsa Veicoli |
| **Autore (PO / Analyst)** | Federico Chiappa |
| **Assegnatario (Dev)** | Team Dev |
| **Sprint / Iterazione** | Sprint 1 |
| **Stima (Story Points)** | 3 |
| **Stato** | Ready for Dev |

---

### 1. Dichiarazione della Storia (Formulato Connextra)

> **Come** Utente registrato e autenticato  
> **voglio** richiedere lo sblocco del veicolo selezionato tramite l'app mobile  
> **affinché** io possa iniziare la mia corsa in totale autonomia senza utilizzare chiavi fisiche.

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

#### Scenario 1: Sblocco Veicolo con Successo (Happy Path)
```gherkin
Scenario: Sblocco completato con successo
  Given l'utente autenticato si trova entro 50 metri dal veicolo selezionato "CAR-102"
  And il veicolo "CAR-102" è nello stato "DISPONIBILE"
  And l'utente possiede un metodo di pagamento valido pre-autorizzabile per 5.00 EUR
  When l'utente seleziona "Sblocca Veicolo" nell'applicazione
  Then il sistema pre-autorizza 5.00 EUR sul metodo di pagamento
  And invia il comando MQTT di sblocco al veicolo
  And imposta lo stato del veicolo in "IN_USO"
  And mostra il timer di corsa attivo sull'interfaccia utente
```

#### Scenario 2: Utente troppo lontano dal veicolo (Edge / Error Path)
```gherkin
Scenario: Tentativo di sblocco fuori dal raggio di prossimità
  Given l'utente si trova a 150 metri dal veicolo "CAR-102"
  When l'utente tenta di premere il pulsante "Sblocca Veicolo"
  Then il sistema rifiuta l'invio del comando hardware
  And mostra un messaggio di errore "Avvicinati al veicolo (entro 50m) per procedere allo sblocco"
  And non addebita alcuna pre-autorizzazione sulla carta dell'utente
```

---

### 4. Note Tecniche e Dipendenze
* **Endpoint API di Riferimento:** `POST /api/v1/rentals/start` (OpenAPI Spec).
* **Componenti UI / Wireframe:** Schermata Mappa e Modal di Conferma Sblocco (Prototipo Figma).
* **Vincoli Dati / Entità Coinvolte:** Tabelle `rentals`, `vehicles`, `payment_tokens` con gestione di locks transazionali su veicolo.

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
