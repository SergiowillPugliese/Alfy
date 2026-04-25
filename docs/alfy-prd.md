# PRD — Alfy: Il Maggiordomo Digitale

**Versione:** 0.1 (Draft)
**Data:** Marzo 2026
**Autore:** Sergio
**Stato:** In revisione

---

## 1. Visione del Prodotto

Alfy è un maggiordomo digitale AI-first progettato per supportare singoli e famiglie nella gestione della vita quotidiana. A differenza delle app tradizionali basate su dashboard e interazioni manuali, Alfy si presenta come un assistente conversazionale con cui l'utente dialoga in linguaggio naturale. Alfy interpreta le intenzioni, attiva le funzionalità appropriate e risponde in modo proattivo, dando la percezione di avere un assistente personale sempre disponibile.

Il prodotto è pensato sia per uso personale che come progetto open source da includere in un portfolio professionale.

---

## 2. Problema che Alfy risolve

Le app di gestione familiare esistenti sono frammentate, macchinose e richiedono all'utente di imparare interfacce complesse. Il risultato è che vengono abbandonate dopo poche settimane. Alfy abbassa la barriera d'ingresso portando l'interazione al livello più naturale possibile: la conversazione. L'utente non deve sapere dove si trova una funzione — la chiede e basta.

---

## 3. Utenti Target

### Utente primario — Il genitore organizzatore
Persona tra i 30 e i 50 anni, con famiglia, poco tempo, che gestisce spese, appuntamenti, liste e documenti per sé e per gli altri. Vuole delegare la complessità organizzativa senza imparare nuovi strumenti.

### Utente secondario — Il partner/membro della famiglia
Accede ad Alfy per consultare le cose che lo riguardano, aggiungere elementi condivisi o ricevere notifiche. Meno coinvolto nella configurazione, più nell'uso quotidiano.

### Utente terziario — Il single
Una persona sola che vuole un assistente personale per tenere sotto controllo la propria vita senza la complessità del modulo familiare.

---

## 4. Obiettivi del Prodotto

| Obiettivo | Metrica di successo |
|-----------|-------------------|
| Ridurre il tempo speso a gestire la vita domestica | Utilizzo quotidiano da parte dell'utente principale |
| Offrire un'esperienza conversazionale naturale | Tasso di completamento delle richieste via chat |
| Supportare la dimensione familiare | Almeno 2 profili attivi per nucleo familiare |
| Essere un progetto portfolio di qualità | Documentazione completa, codice su GitHub, README professionale |

---

## 5. Macro-Funzionalità

### F1 — Core AI: Alfy
Il motore conversazionale dell'applicazione. Alfy interpreta le richieste in linguaggio naturale, mantiene una memoria persistente dell'utente e della famiglia nel tempo, e attiva gli strumenti applicativi appropriati (tool use). È il layer che unifica tutte le altre funzionalità. Senza F1, nessun'altra funzionalità ha senso.

### F2 — Gestione Utenti e Famiglia
Sistema di autenticazione e profili. Ogni utente ha un profilo personale con dati privati. Esiste un profilo famiglia condiviso con ruoli (admin, membro) e permessi che definiscono cosa è visibile a tutti e cosa è personale.

### F3 — Spese e Budget
Tracciamento di entrate e uscite, categorie personalizzabili, budget mensili, possibilità di associare una spesa a un singolo membro o all'intera famiglia. Vista personale e vista aggregata familiare.

### F4 — Agenda e Appuntamenti
Calendario con eventi personali e condivisi, promemoria, eventi ricorrenti. Possibile integrazione con calendari esterni (Google Calendar).

### F5 — Liste e Task
Liste della spesa, to-do personali e familiari, deleghe ad altri membri. Gestione degli stati (da fare, in corso, completato).

### F6 — Documenti e Ricevute
Archiviazione di file (foto, PDF), ricevute, garanzie, documenti importanti. I documenti sono ricercabili e accessibili via conversazione con Alfy.

### F7 — Notifiche Proattive
Alfy notifica l'utente in autonomia per scadenze, bollette, appuntamenti imminenti, manutenzioni programmate e ricorrenze. L'utente non deve ricordarsi di chiedere.

### F8 — Casa e Manutenzioni
Registro degli interventi sulla casa e sui veicoli, scadenze periodiche (caldaia, bollo, assicurazioni), storico dei lavori eseguiti.

### F9 — Salute e Benessere
Appuntamenti medici, gestione farmaci con posologia e scadenze, storico sanitario per ogni membro della famiglia.

### F10 — Hub Familiare (Modalità Tablet)
Interfaccia dedicata per un dispositivo condiviso posizionato in casa (es. tablet all'ingresso). Mostra una vista aggregata degli eventi del giorno, liste attive, notifiche familiari. Accesso con utenza famiglia condivisa.

### F11 — Smart Home (Integrazione Esterna)
Integrazione con sistemi di domotica (Home Assistant, Google Home, protocollo Matter) per controllare dispositivi domestici tramite Alfy. Luci, elettrodomestici, sicurezza. Funzionalità condizionata alla disponibilità di un sistema smart home nell'abitazione dell'utente.

---

## 6. Fuori Scope (v1.0)

- Integrazione con istituti bancari o fintech (es. import automatico estratto conto)
- Gestione contabile avanzata o dichiarazione dei redditi
- Funzionalità social o condivisione con persone esterne alla famiglia
- Marketplace o acquisti in-app
- Supporto multilingua (v1.0 solo italiano)

---

## 7. Requisiti Non Funzionali

- **Disponibilità:** l'app deve funzionare offline per la consultazione dei dati già sincronizzati
- **Privacy:** i dati sensibili (salute, documenti) non devono essere inviati a terze parti senza consenso esplicito
- **Scalabilità:** l'architettura deve supportare da 1 a 6 membri per nucleo familiare senza degradazione
- **Accessibilità:** interfaccia utilizzabile anche da utenti non tecnici (es. anziani in famiglia)
- **Open Source:** il codice deve essere ben documentato, con README chiaro e licenza aperta

---

## 8. Vincoli di Progetto

- Sviluppo da parte di un singolo sviluppatore
- Nessun Mac disponibile per build iOS nativa tradizionale
- Budget limitato per servizi cloud (preferenza per tier gratuiti o open source self-hostable)
- Obiettivo portfolio: il codice deve essere leggibile e la documentazione completa

---

## 9. Dipendenze Esterne

| Dipendenza | Tipo | Note |
|-----------|------|-------|
| Claude API (Anthropic) | AI conversazionale e tool use | Core del prodotto |
| Google Calendar API | Opzionale | Integrazione agenda |
| Home Assistant / Google Home | Opzionale | Solo F11 |
| Servizio di notifiche push | Da definire | Necessario per F7 |

---

## 10. Roadmap ad Alto Livello

| Fase | Contenuto | Priorità |
|------|-----------|----------|
| **Fase 1 — Core** | F1 (AI), F2 (Utenti/Famiglia) | Bloccante |
| **Fase 2 — Gestione quotidiana** | F3 (Spese), F4 (Agenda), F5 (Liste) | Alta |
| **Fase 3 — Archivio e salute** | F6 (Documenti), F8 (Casa), F9 (Salute) | Media |
| **Fase 4 — Proattività** | F7 (Notifiche proattive) | Media |
| **Fase 5 — Espansione** | F10 (Hub Tablet), F11 (Smart Home) | Bassa / Futura |

---

*Documento soggetto a revisione. Le decisioni tecnologiche (stack, database, infrastruttura) sono trattate separatamente nel documento di Architettura Tecnica.*
