# Roadmap di Sviluppo — Alfy: Il Maggiordomo Digitale

**Versione:** 0.1 (Draft)
**Data:** Marzo 2026
**Autore:** Sergio
**Stato:** In revisione

---

## Principi della Roadmap

- **Una tecnologia nuova alla volta** — ogni fase introduce concetti nuovi in modo controllato.
- **Ogni fase è utile da sola** — al termine di ogni fase, Alfy funziona già in qualcosa di concreto.
- **Prima la profondità, poi l'ampiezza** — meglio una funzionalità ben fatta che tre mezze.
- **Il codice è l'ultimo passo** — ogni funzionalità viene prima capita, poi costruita.

---

## Fase 0 — Setup e Fondamenta
**Obiettivo:** avere un ambiente di sviluppo funzionante e un'app vuota che gira sul telefono.
**Durata stimata:** 1-2 settimane
**Tecnologie introdotte:** Expo, React Native, TypeScript, Supabase CLI, GitHub

### Attività
- [ ] Creare repository GitHub con struttura monorepo (`alfy/`)
- [ ] Inizializzare progetto Expo con TypeScript
- [ ] Installare e configurare Supabase CLI in locale
- [ ] Creare progetto Supabase (hosted)
- [ ] Connettere l'app Expo a Supabase
- [ ] Caricare tutta la documentazione nella cartella `docs/`
- [ ] Scrivere il `README.md` iniziale del progetto
- [ ] Installare Expo Go su iPhone e testare l'app sul dispositivo fisico

### Deliverable
App vuota con schermata di benvenuto che gira su iPhone (tramite Expo Go) e browser. Repository GitHub pubblico con documentazione completa.

### Cosa impari
Come funziona un progetto React Native, cosa fa Expo, come si struttura un monorepo, come si usa Git in modo professionale.

> **Nota iOS:** per i test quotidiani si usa Expo Go su iPhone (App Store, gratuito). Per generare la build finale da pubblicare sull'App Store si usa EAS Build — un servizio cloud di Expo che compila su server Mac remoti, senza bisogno di un Mac fisico. Il tier gratuito è sufficiente per uso personale.

---

## Fase 1 — Autenticazione e Famiglia
**Obiettivo:** un utente può registrarsi, accedere, creare un nucleo familiare e invitare un altro membro.
**Durata stimata:** 2-3 settimane
**Tecnologie introdotte:** Supabase Auth, PostgreSQL (prime tabelle), Row Level Security

### Attività
- [ ] Creare le tabelle `USER` e `FAMILY` nel database
- [ ] Implementare registrazione e login con email/password tramite Supabase Auth
- [ ] Implementare la creazione di un nucleo familiare
- [ ] Implementare il sistema di invito tramite codice
- [ ] Implementare i ruoli (admin / membro)
- [ ] Configurare Row Level Security — ogni utente vede solo i propri dati
- [ ] Implementare la schermata profilo utente

### Deliverable
Alfy funziona con autenticazione reale. Si può creare una famiglia, generare un codice invito e usarlo da un secondo dispositivo per unirsi.

### Cosa impari
Come funziona l'autenticazione JWT, cosa sono le policy RLS in PostgreSQL, come si gestisce lo stato di autenticazione in React Native.

---

## Fase 2 — La Chat con Alfy (Core AI)
**Obiettivo:** avere una conversazione reale con Alfy, che risponde con personalità e ricorda chi sei.
**Durata stimata:** 3-4 settimane
**Tecnologie introdotte:** Claude API, Supabase Edge Functions, sistema di memoria (tabella MEMORY)

### Attività
- [ ] Creare le tabelle `CONVERSATION`, `MESSAGE` e `MEMORY`
- [ ] Scrivere la prima Edge Function: `ai-handler`
- [ ] Integrare Claude API con tool use (inizialmente zero tool — solo conversazione)
- [ ] Implementare il system prompt con iniezione della memoria persistente
- [ ] Implementare l'interfaccia chat nell'app (lista messaggi + input)
- [ ] Implementare il tool `update_memory` — Alfy può salvare informazioni su di te
- [ ] Testare la persistenza della memoria tra sessioni diverse

### Deliverable
Si può parlare con Alfy. Lui risponde con tono caldo e personale, ricorda il tuo nome e le informazioni che gli hai dato nelle sessioni precedenti.

### Cosa impari
Cosa sono le Edge Functions e come funzionano, come si usa il tool use di Claude, cosa è un system prompt, come si gestisce il costo dei token.

---

## Fase 3 — Spese e Budget
**Obiettivo:** Alfy può registrare spese, rispondere a domande sulle finanze e avvisare quando ci si avvicina al budget.
**Durata stimata:** 2-3 settimane
**Tecnologie introdotte:** Query SQL più complesse, tool use applicato al database

### Attività
- [ ] Creare le tabelle `EXPENSE` e `BUDGET`
- [ ] Implementare i tool: `create_expense`, `get_expenses_summary`
- [ ] Implementare la gestione del budget mensile per categoria
- [ ] Implementare la distinzione spese personali / familiari
- [ ] Aggiungere una schermata opzionale di riepilogo spese (non obbligatoria — si può fare tutto via chat)
- [ ] Testare scenari reali: "ho speso 30€ al supermercato", "quanto ho speso questo mese?"

### Deliverable
Alfy gestisce le spese tramite conversazione. Registra, categorizza, riepiloga e avvisa quando si supera il budget.

### Cosa impari
Come si scrivono query SQL aggregate (SUM, GROUP BY), come i tool di Claude interagiscono con il database reale.

---

## Fase 4 — Agenda e Appuntamenti
**Obiettivo:** Alfy gestisce il calendario personale e familiare tramite conversazione.
**Durata stimata:** 2-3 settimane
**Tecnologie introdotte:** Gestione date e ricorrenze (formato iCal), eventi condivisi

### Attività
- [ ] Creare le tabelle `EVENT` e `EVENT_PARTICIPANT`
- [ ] Implementare i tool: `create_event`, `get_events`
- [ ] Implementare gli eventi ricorrenti con `recurrence_rule`
- [ ] Implementare la distinzione eventi personali / condivisi
- [ ] Implementare una schermata calendario opzionale
- [ ] Valutare integrazione Google Calendar (opzionale in questa fase)

### Deliverable
Alfy aggiunge e recupera appuntamenti tramite conversazione. Gli eventi condivisi sono visibili a tutti i membri della famiglia.

### Cosa impari
Come si gestiscono date e timezone in un'app, cosa sono gli eventi ricorrenti e il formato iCal, come funzionano le relazioni molti-a-molti nel database.

---

## Fase 5 — Liste e Task
**Obiettivo:** Alfy gestisce liste della spesa, to-do e deleghe familiari.
**Durata stimata:** 1-2 settimane
**Tecnologie introdotte:** Realtime di Supabase (aggiornamenti live tra dispositivi)

### Attività
- [ ] Creare le tabelle `LIST` e `TASK`
- [ ] Implementare i tool: `create_task`, `complete_task`, `get_list`
- [ ] Implementare l'assegnazione di task a un membro della famiglia
- [ ] Implementare il realtime — quando un membro aggiorna la lista, gli altri la vedono subito
- [ ] Implementare le notifiche push per i task assegnati

### Deliverable
La lista della spesa è condivisa e aggiornata in tempo reale tra i dispositivi della famiglia. Alfy assegna task e notifica il membro interessato.

### Cosa impari
Come funziona il realtime con WebSocket, come si inviano notifiche push con Expo, come si gestiscono i permessi di notifica su iOS e Android.

---

## Fase 6 — Notifiche Proattive
**Obiettivo:** Alfy contatta l'utente in autonomia, senza aspettare che venga interpellato.
**Durata stimata:** 2 settimane
**Tecnologie introdotte:** Supabase Scheduled Functions (cron job), logica di scheduling

### Attività
- [ ] Creare la tabella `NOTIFICATION`
- [ ] Scrivere la Edge Function `scheduler` — gira ogni mattina
- [ ] Implementare il "buongiorno" con riepilogo del giorno
- [ ] Implementare le notifiche per scadenze documentali, manutenzioni, compleanni
- [ ] Implementare le notifiche per avvicinamento al budget mensile
- [ ] Implementare le preferenze di notifica per utente (cosa ricevere e con quanto anticipo)

### Deliverable
Ogni mattina Alfy manda un riepilogo della giornata. L'utente riceve avvisi proattivi per scadenze e budget senza dover chiedere nulla.

### Cosa impari
Cosa sono i cron job e come si pianificano task ricorrenti, come si gestisce la logica temporale complessa in un'applicazione.

---

## Fase 7 — Documenti, Casa e Salute
**Obiettivo:** Alfy archivia documenti, gestisce manutenzioni e tiene il registro sanitario della famiglia.
**Durata stimata:** 3 settimane
**Tecnologie introdotte:** Supabase Storage (upload file), gestione immagini in React Native

### Attività
- [ ] Creare le tabelle `DOCUMENT`, `MAINTENANCE`, `HEALTH_RECORD`, `MEDICATION`
- [ ] Implementare upload di foto e PDF tramite Supabase Storage
- [ ] Implementare i tool: `save_document`, `search_documents`, `create_maintenance`, `save_health_record`
- [ ] Implementare la ricerca documenti via chat ("dove ho messo la garanzia del frigo?")
- [ ] Implementare le notifiche per scadenze documentali e manutenzioni
- [ ] Assicurare che i dati sanitari siano visibili solo al proprietario

### Deliverable
Alfy archivia e trova documenti, ricorda le manutenzioni in scadenza e gestisce il registro sanitario familiare. Tutto accessibile via conversazione.

### Cosa impari
Come si gestisce l'upload di file in un'app mobile, come funziona lo storage cloud, come si implementa la ricerca testuale in PostgreSQL.

---

## Fase 8 — Hub Familiare (Modalità Tablet)
**Obiettivo:** una schermata dedicata per il tablet condiviso di casa, sempre accesa, sempre aggiornata.
**Durata stimata:** 2 settimane
**Tecnologie introdotte:** Layout responsive adattivo, modalità kiosk

### Attività
- [ ] Progettare una UI dedicata ottimizzata per tablet (landscape, testo grande)
- [ ] Implementare l'utenza famiglia condivisa senza login personale
- [ ] Implementare la vista aggregata: eventi del giorno, liste attive, notifiche familiari
- [ ] Implementare la chat con Alfy dall'Hub (richieste rapide familiari)
- [ ] Configurare la modalità kiosk (schermo sempre acceso, nessuna navigazione di sistema)

### Deliverable
Un tablet all'ingresso di casa mostra in tempo reale lo stato della famiglia. Chiunque può interagire con Alfy senza autenticarsi con il proprio profilo.

### Cosa impari
Come si progetta una UI adattiva per form factor diversi, come si gestiscono sessioni condivise, cosa è la modalità kiosk.

---

## Fase 9 — Smart Home (Integrazione Esterna)
**Obiettivo:** Alfy controlla i dispositivi smart di casa tramite conversazione.
**Durata stimata:** 3 settimane (condizionata alla disponibilità di dispositivi smart)
**Tecnologie introdotte:** Home Assistant API / Google Home API, integrazione webhook

### Attività
- [ ] Creare la tabella `SMART_HOME_DEVICE`
- [ ] Implementare il tool: `control_smart_device`
- [ ] Integrare con Home Assistant tramite API REST
- [ ] Implementare la discovery dei dispositivi disponibili
- [ ] Testare scenari reali: luci, prese smart, elettrodomestici

### Deliverable
Alfy controlla i dispositivi smart della casa tramite conversazione. "Spegni le luci del salotto" funziona.

### Cosa impari
Come funzionano le API REST di terze parti, cosa sono i webhook, come si integra un sistema esterno in modo sicuro.

---

## Riepilogo Fasi

| Fase | Contenuto | F. coperte | Stima |
|------|-----------|-----------|-------|
| **0** | Setup e fondamenta | — | 1-2 sett. |
| **1** | Autenticazione e famiglia | F2 | 2-3 sett. |
| **2** | Chat con Alfy (Core AI) | F1 | 3-4 sett. |
| **3** | Spese e budget | F3 | 2-3 sett. |
| **4** | Agenda e appuntamenti | F4 | 2-3 sett. |
| **5** | Liste e task | F5 | 1-2 sett. |
| **6** | Notifiche proattive | F7 | 2 sett. |
| **7** | Documenti, casa e salute | F6, F8, F9 | 3 sett. |
| **8** | Hub familiare | F10 | 2 sett. |
| **9** | Smart home | F11 | 3 sett. |
| | **Totale stimato** | | **21-29 sett.** |

---

## Note sulle Stime

Le stime sono indicative e assumono un ritmo di sviluppo part-time (8-10 ore settimanali). Non includono:
- Tempo di apprendimento delle tecnologie nuove (variabile)
- Bug fixing e refactoring
- Iterazioni sul design dell'interfaccia

È normale che alcune fasi richiedano il doppio del tempo stimato. L'obiettivo non è la velocità — è costruire qualcosa di solido che si capisce.

---

## Milestone di Portfolio

Questi sono i punti in cui il progetto è già presentabile in un contesto professionale:

| Milestone | Dopo la fase | Cosa mostra |
|-----------|-------------|-------------|
| **M1 — MVP conversazionale** | Fase 2 | Architettura AI con tool use, integrazione Claude API, memoria persistente |
| **M2 — App funzionante** | Fase 5 | Prodotto reale con auth, database, notifiche, multi-utente |
| **M3 — Prodotto completo** | Fase 7 | Full stack con storage, logica complessa, privacy dei dati |
| **M4 — Visione completa** | Fase 9 | Integrazione IoT, Hub tablet, sistema domestico completo |

---

*Documento soggetto a revisione. La roadmap verrà aggiornata al termine di ogni fase in base a quanto appreso durante lo sviluppo.*
