# Architettura Tecnica — Alfy: Il Maggiordomo Digitale

**Versione:** 0.1 (Draft)
**Data:** Marzo 2026
**Autore:** Sergio
**Stato:** In revisione

---

## 1. Principi Guida

Le scelte tecnologiche di Alfy sono guidate da questi criteri, in ordine di priorità:

1. **Semplicità operativa** — un singolo sviluppatore deve poter costruire, testare e mantenere il sistema senza infrastruttura complessa.
2. **Costo contenuto** — preferenza per tier gratuiti o costi minimi per uso personale.
3. **Qualità portfolio** — lo stack deve essere moderno, leggibile e giustificabile in un colloquio tecnico.
4. **Scalabilità futura** — le scelte non devono precludere una crescita del progetto, anche se non è l'obiettivo immediato.
5. **Un solo linguaggio** — TypeScript su tutto, per ridurre il contesto mentale durante lo sviluppo.

---

## 2. Stack Tecnologico

| Layer | Tecnologia | Motivazione |
|-------|-----------|-------------|
| **Frontend mobile/web** | React Native + Expo | Unico codebase per iOS, Android e Web. Build iOS senza Mac tramite EAS Cloud. Ecosistema maturo, ottima integrazione con Supabase e TypeScript. |
| **Database** | Supabase (PostgreSQL) | Database relazionale managed, coerente con l'ERD progettato. Tier gratuito generoso. Open source e self-hostabile in futuro se necessario. |
| **Autenticazione** | Supabase Auth | Incluso in Supabase. Supporta email/password e OAuth (Google). Nessun servizio esterno aggiuntivo. |
| **Storage file** | Supabase Storage | Incluso in Supabase. Gestisce upload di documenti, ricevute e foto. Tier gratuito: 1GB. |
| **Backend logic** | Supabase Edge Functions | Funzioni serverless in TypeScript per logica complessa (es. orchestrazione AI, notifiche pianificate). Nessun server da gestire. |
| **AI conversazionale** | Claude API (Anthropic) | Motore conversazionale con tool use per attivare le funzionalità di Alfy. Modello: claude-haiku (veloce, economico per uso quotidiano) con fallback a claude-sonnet per richieste complesse. |
| **Notifiche push** | Expo Notifications | Incluso nell'ecosistema Expo. Funziona su iOS e Android senza servizi esterni. |
| **Linguaggio** | TypeScript | Usato su tutto lo stack. Riduce gli errori, migliora la leggibilità del codice per il portfolio. |

---

## 3. Architettura del Sistema

```
┌─────────────────────────────────────────────────────────┐
│                        CLIENT                           │
│                                                         │
│   ┌─────────────────┐       ┌─────────────────┐        │
│   │   App Mobile    │       │   App Web       │        │
│   │ (iOS / Android) │       │   (Browser)     │        │
│   └────────┬────────┘       └────────┬────────┘        │
│            └──────────┬─────────────┘                  │
│                       │ React Native + Expo             │
└───────────────────────┼─────────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────────┐
│                      SUPABASE                           │
│                                                         │
│   ┌──────────────┐  ┌──────────────┐  ┌─────────────┐  │
│   │  PostgreSQL  │  │     Auth     │  │   Storage   │  │
│   │  (database)  │  │  (utenti)    │  │  (file)     │  │
│   └──────────────┘  └──────────────┘  └─────────────┘  │
│                                                         │
│   ┌─────────────────────────────────────────────────┐   │
│   │              Edge Functions (TypeScript)        │   │
│   │                                                 │   │
│   │  ┌─────────────┐     ┌──────────────────────┐  │   │
│   │  │ AI Handler  │────▶│   Claude API          │  │   │
│   │  │             │     │   (tool use)          │  │   │
│   │  └─────────────┘     └──────────────────────┘  │   │
│   │                                                 │   │
│   │  ┌─────────────┐     ┌──────────────────────┐  │   │
│   │  │ Notif.      │────▶│   Expo Push           │  │   │
│   │  │ Scheduler   │     │   Notifications       │  │   │
│   │  └─────────────┘     └──────────────────────┘  │   │
│   └─────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
```

---

## 4. Il Sistema AI — Come Funziona Alfy

Questa è la parte più critica dell'architettura. Alfy non è un semplice chatbot — è un agente che usa il **tool use** di Claude per interagire con il database.

### Flusso di una conversazione

```
Utente: "Ho speso 45€ al supermercato oggi"
         │
         ▼
   Edge Function: AI Handler
         │
         ├─ Carica memoria persistente dell'utente (tabella MEMORY)
         ├─ Carica ultime N righe della conversazione (tabella MESSAGE)
         ├─ Prepara lista di tool disponibili
         │
         ▼
   Claude API (claude-haiku)
         │
         ├─ Analizza il messaggio
         ├─ Decide di chiamare il tool: create_expense
         │   └─ parametri: { amount: 45, category: "alimentari", date: oggi }
         │
         ▼
   Edge Function: esegue create_expense su PostgreSQL
         │
         ▼
   Claude API: riceve conferma, formula risposta
         │
         ▼
   Utente: "Fatto! Ho registrato 45€ per alimentari. 
            Questo mese hai speso 312€ in questa categoria."
```

### Tool disponibili per Alfy (lista iniziale)

| Tool | Descrizione |
|------|-------------|
| `create_expense` | Registra una nuova spesa |
| `get_expenses_summary` | Recupera riepilogo spese per periodo/categoria |
| `create_event` | Aggiunge un appuntamento al calendario |
| `get_events` | Recupera eventi per data o periodo |
| `create_task` | Aggiunge un task a una lista |
| `complete_task` | Segna un task come completato |
| `get_list` | Recupera il contenuto di una lista |
| `save_document` | Archivia un documento |
| `search_documents` | Cerca tra i documenti archiviati |
| `create_maintenance` | Registra un intervento di manutenzione |
| `get_maintenance_schedule` | Recupera le manutenzioni in scadenza |
| `save_health_record` | Registra un evento sanitario |
| `update_memory` | Aggiorna la memoria persistente di Alfy |
| `control_smart_device` | Invia comando a dispositivo smart home |

### Memoria persistente

Ad ogni conversazione, l'AI Handler carica la tabella MEMORY filtrata per l'utente corrente. Questo context viene iniettato nel system prompt di Claude, permettendo ad Alfy di ricordare informazioni nel tempo senza dipendere dalla cronologia dei messaggi (che viene troncata per ragioni di costo).

Esempio di system prompt con memoria:
```
Sei Alfy, il maggiordomo digitale di Sergio.
Quello che sai di Sergio:
- allergie: nichel
- giorno_stipendio: 27
- macchina: Fiat 500, targa AB123CD
- animale_domestico: Luna, gatta, 3 anni
Oggi è [data]. Rispondi sempre in italiano, con tono caldo e personale.
```

---

## 5. Gestione dei Costi Claude API

Essendo l'AI il componente a costo variabile, è importante gestirlo con attenzione.

| Strategia | Descrizione |
|-----------|-------------|
| **Modello primario** | `claude-haiku` — veloce ed economico per le richieste quotidiane |
| **Modello secondario** | `claude-sonnet` — usato solo per richieste complesse o ambigue |
| **Troncamento contesto** | Le conversazioni vengono troncate alle ultime 20 righe prima di inviare a Claude |
| **Memoria separata** | Le informazioni persistenti vivono nella tabella MEMORY, non nella cronologia messaggi |
| **Caching system prompt** | Il system prompt con la memoria viene cachato lato Anthropic (prompt caching) per ridurre i token di input |

---

## 6. Sicurezza e Privacy

| Area | Soluzione |
|------|-----------|
| **Autenticazione** | Supabase Auth con JWT. Token refresh automatico. |
| **Autorizzazione** | Row Level Security (RLS) di PostgreSQL — ogni utente vede solo i propri dati o quelli della sua famiglia. |
| **Dati sanitari** | Visibili solo all'utente proprietario, mai condivisi con altri membri senza consenso esplicito. |
| **Chiave API Claude** | Conservata come variabile d'ambiente nelle Edge Functions, mai esposta al client. |
| **File archiviati** | Accesso tramite URL firmati con scadenza (Supabase Storage signed URLs). |

---

## 7. Struttura del Progetto (Monorepo)

```
alfy/
├── apps/
│   └── mobile/          # React Native + Expo (iOS, Android, Web)
├── packages/
│   └── types/           # Tipi TypeScript condivisi
├── supabase/
│   ├── migrations/      # Migrazioni del database
│   ├── functions/       # Edge Functions
│   │   ├── ai-handler/  # Orchestrazione Claude API
│   │   └── scheduler/   # Notifiche proattive pianificate
│   └── seed.sql         # Dati di esempio per sviluppo
├── docs/                # Documentazione del progetto
│   ├── PRD.md
│   ├── user-stories.md
│   ├── ERD.md
│   └── architecture.md  # Questo documento
└── README.md
```

---

## 8. Strumenti di Sviluppo

| Strumento | Uso |
|-----------|-----|
| **Cursor** | IDE AI-assisted per lo sviluppo |
| **Supabase CLI** | Gestione locale del database e delle funzioni |
| **Expo Go** | Test rapido su dispositivo fisico Android durante lo sviluppo |
| **EAS Build** | Build cloud per iOS (senza Mac) |
| **GitHub** | Version control e portfolio |
| **GitHub Actions** | CI/CD per deploy automatico |

---

## 9. Note su Scelte Non Adottate

| Alternativa | Motivo della non scelta |
|-------------|------------------------|
| **Flutter** | Richiede apprendimento di Dart, vantaggio non sufficiente rispetto a React Native per questo progetto |
| **Firebase** | Database NoSQL non adatto alla struttura relazionale dell'ERD. Costi imprevedibili. Closed source. |
| **Backend custom (Node/NestJS)** | Aggiunge complessità infrastrutturale non necessaria per un singolo sviluppatore. Supabase Edge Functions coprono i casi d'uso richiesti. |
| **Next.js** | Ottimo per web-first, ma penalizza l'esperienza mobile rispetto a React Native. |
| **Self-hosting** | Complessità eccessiva per la fase attuale del progetto. Supabase è self-hostabile in futuro se necessario. |

---

*Documento soggetto a revisione. Le decisioni architetturali potranno essere rivalutate al manifestarsi di nuove esigenze o vincoli.*
