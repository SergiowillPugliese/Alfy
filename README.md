# Alfy — Il Maggiordomo Digitale

Un assistente personale AI-first per la gestione della vita quotidiana di singoli e famiglie.

## Cos'è Alfy

Alfy è una web app installabile sul telefono (PWA) dove l'interfaccia principale è una **conversazione in linguaggio naturale**. Invece di navigare menu e form, l'utente parla con Alfy come farebbe con un vero maggiordomo:

> "Ho speso 45 euro al supermercato oggi"
> "Cosa ho in agenda questa settimana?"
> "Aggiungi latte e pane alla lista della spesa"

Alfy interpreta la richiesta, esegue l'azione sul database tramite **tool use** (Claude API), e risponde in modo naturale.

## Funzionalità (previste)

- **Chat AI** — Conversazione naturale con memoria persistente
- **Spese e Budget** — Tracciamento entrate/uscite, budget per categoria
- **Agenda** — Calendario personale e familiare, eventi ricorrenti
- **Liste e Task** — Lista della spesa, to-do, deleghe familiari
- **Documenti** — Archiviazione ricevute, garanzie, documenti importanti
- **Notifiche proattive** — Alfy ti avvisa senza che tu debba chiedere
- **Casa e Manutenzioni** — Registro interventi, scadenze programmate
- **Salute** — Appuntamenti medici, farmaci, registro sanitario

## Stack Tecnologico

| Layer | Tecnologia |
|-------|-----------|
| Frontend | Angular, distribuito come PWA |
| Navigazione | Angular Router |
| Notifiche | Web Push (service worker) |
| Database | Supabase (PostgreSQL) |
| Autenticazione | Supabase Auth |
| Storage | Supabase Storage |
| Backend | Supabase Edge Functions (TypeScript) |
| AI | Claude API (Anthropic) con tool use |
| Linguaggio | TypeScript su tutto lo stack |

## Prerequisiti

> **Migrazione in corso** ([ADR 0001](./docs/adr/0001-angular-pwa-invece-di-react-native.md)): il prototipo React Native + Expo è stato rimosso e il codice attuale è lo scaffold Angular generato da `ng new`. Prerequisiti, setup e struttura qui sotto descrivono ancora il prototipo e verranno aggiornati a migrazione completata.

- [Node.js](https://nodejs.org/) v20.19.4+ (minimo richiesto da React Native 0.81)
- [Expo Go](https://expo.dev/go) installato sul dispositivo mobile (per test su telefono)
- Un account [Supabase](https://supabase.com/) con un progetto creato

## Setup locale

```bash
# Clona il repository
git clone https://github.com/SergiowillPugliese/Alfy.git
cd Alfy

# Installa le dipendenze
npm install

# Configura le variabili d'ambiente
cp .env.example .env
# Modifica .env con le tue chiavi Supabase (vedi sotto)

# Avvia il dev server
npm start
```

### Variabili d'ambiente

| Variabile | Dove trovarla (dashboard Supabase) |
|-----------|-------------------------------------|
| `EXPO_PUBLIC_SUPABASE_URL` | Project Settings → Data API → Project URL |
| `EXPO_PUBLIC_SUPABASE_KEY` | Project Settings → API Keys → **Publishable key** (`sb_publishable_...`) |

> **Attenzione:** le variabili con prefisso `EXPO_PUBLIC_` vengono incluse nel bundle JavaScript dell'app, quindi chiunque abbia l'app può leggerle. Usa **solo** la publishable key. La secret key (`sb_secret_...`) o la vecchia `service_role` ignorano la Row Level Security e non devono mai finire nel client.

Le variabili vengono lette all'avvio del dev server: dopo aver modificato `.env` riavvia `npm start`. Se i valori non si aggiornano, usa `npx expo start --clear`.

Dopo l'avvio:
- Premi `w` per aprire nel browser
- Scansiona il QR code con la fotocamera dell'iPhone per aprire in Expo Go
- Premi `a` per aprire nell'emulatore Android (se configurato)

## Struttura del progetto

```
alfy/
├── app/                 # Schermate (Expo Router file-based routing)
│   ├── _layout.tsx      # Layout root (Stack navigator)
│   └── (tabs)/          # Navigazione a tab
│       ├── _layout.tsx  # Configurazione tab bar
│       ├── index.tsx    # Home
│       ├── chat.tsx     # Chat con Alfy
│       └── profile.tsx  # Profilo utente
├── lib/                 # Utility e configurazioni
│   └── supabase.ts      # Client Supabase
├── assets/              # Immagini e icone
├── docs/                # Documentazione di progetto
└── app.json             # Configurazione Expo
```

## Documentazione

La documentazione completa del progetto si trova nella cartella [`docs/`](./docs/):

- [PRD](./docs/alfy-prd.md) — Product Requirements Document
- [Architettura](./docs/alfy-architecture.md) — Architettura tecnica
- [ERD](./docs/alfy-erd.md) — Entity Relationship Diagram
- [Roadmap](./docs/alfy-roadmap.md) — Roadmap di sviluppo
- [User Stories](./docs/alfy-user-stories.md) — User stories per feature
- [Indice e decisioni architetturali (ADR)](./docs/index.md)

## Stato del progetto

**Fase in corso:** 0 — Setup e Fondamenta, riaperta per la migrazione del frontend ad Angular PWA
**Prossima fase:** 1 — Autenticazione e Famiglia

Vedi la [roadmap completa](./docs/alfy-roadmap.md) per i dettagli sulle fasi successive.

## Licenza

MIT
