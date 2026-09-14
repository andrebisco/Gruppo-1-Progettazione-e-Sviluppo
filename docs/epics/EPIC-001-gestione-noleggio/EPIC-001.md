# EPIC-001: Gestione Noleggio e Flusso Corsa Veicoli

| Campo | Specifica |
| :--- | :--- |
| **ID** | EPIC-001 |
| **Titolo** | Gestione Noleggio e Flusso Corsa Veicoli |
| **Iniziativa / Theme** | Mobilità Condivisa Green |
| **Owner / PM** | Federico Chiappa |
| **Stato** | In Refinement |
| **Target Release / Milestone** | MVP 1.0 |
| **Priorità Strategica** | Must Have / P1 |

---

### 1. Obiettivo Strategico e Business Outcome
* **Problema di Business:** Gli utenti affrontano processi lunghi e macchinosi per prenotare, sbloccare e restituire i veicoli (auto e bici), causando abbandono dell'applicazione, ritardi nell'avvio della corsa e contestazioni sulle tariffe applicate.
* **Valore Atteso:** Offrire un'esperienza di noleggio *seamless* e completamente automatizzata che riduca il tempo di sblocco a pochi secondi e garantisca la tracciabilità accurata di tempo e chilometri percorsi.
* **Metriche di Successo (KPI / OKR):**
  * Metrica 1: Riduzione del tempo medio di presa in carico ed avvio noleggio veicolo < 30 secondi.
  * Metrica 2: Tasso di completamento sblocchi senza fallimento hardware > 99.5%.

---

### 2. Perimetro Funzionale (Scoping)
* **In Scope (Cosa include questa Epic):**
  * Selezione del veicolo da mappa e verifica disponibilità in tempo reale.
  * Invio del comando IoT di sblocco e avvio sessione di noleggio.
  * Monitoraggio della corsa attiva e calcolo della tariffa temporale/chilometrica.
  * Termine della corsa, verifica posizione GPS (aree consentite), invio comando IoT di blocco e addebito finale.
* **Out of Scope (Esclusioni esplicite e differite):**
  * Gestione abbonamenti corporate / flotta aziendale (prevista per Release 2.0).
  * Gestione e rimborso automatico di sanzioni per infrazioni del codice della strada.

---

### 3. Decomposizione in Features
Elenco delle funzionalità collegate che realizzano l'Epic:

| Feature ID | Titolo Feature | Priorità | Stato |
| :--- | :--- | :--- | :--- |
| `FEAT-001` | Prenotazione e Sblocco IoT Veicolo | Must Have | Ready for Dev |
| `FEAT-002` | Chiusura Corsa e Calcolo Tariffa | Must Have | In Refinement |

---

### 4. Rischi e Dipendenze Architetturali
* **Dipendenze Esterne:** Piattaforma centraline IoT fornitore terzo (MQTT Broker), Gateway di Pagamento per la pre-autorizzazione dei fondi.
* **Rischi Tecnici / Compliance:** Zone d'ombra rete cellulare nei parcheggi interrati, tracciamento GPS e conformità GDPR per la localizzazione dell'utente durante la corsa.

---

### 5. Criteri di Completamento (Epic Definition of Done)
- [ ] Tutte le Features e User Stories collegate sono state rilasciate e hanno superato il collaudo UAT.
- [ ] Contratti API conformi alle specifiche OpenAPI.
- [ ] Documentazione tecnica e architetturale aggiornata nel dossier.
- [ ] Metriche KPI verificate in ambiente di staging/pilota.
