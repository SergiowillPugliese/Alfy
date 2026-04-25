# ERD — Alfy: Entity Relationship Diagram

**Versione:** 0.1 (Draft)
**Data:** Marzo 2026
**Autore:** Sergio
**Stato:** In revisione

---

## Diagramma

```mermaid
erDiagram

    USER {
        uuid id PK
        string email
        string password_hash
        string full_name
        string avatar_url
        string role
        uuid family_id FK
        timestamp created_at
        timestamp deleted_at
    }

    FAMILY {
        uuid id PK
        string name
        string invite_code
        timestamp created_at
    }

    MEMORY {
        uuid id PK
        uuid user_id FK
        uuid family_id FK
        string scope
        string key
        text value
        timestamp created_at
        timestamp updated_at
    }

    CONVERSATION {
        uuid id PK
        uuid user_id FK
        timestamp started_at
        timestamp ended_at
    }

    MESSAGE {
        uuid id PK
        uuid conversation_id FK
        string role
        text content
        timestamp created_at
    }

    EXPENSE {
        uuid id PK
        uuid user_id FK
        uuid family_id FK
        string title
        decimal amount
        string currency
        string category
        boolean is_shared
        date date
        timestamp created_at
        timestamp deleted_at
    }

    BUDGET {
        uuid id PK
        uuid user_id FK
        uuid family_id FK
        string category
        decimal amount_limit
        string period
        timestamp created_at
    }

    EVENT {
        uuid id PK
        uuid created_by FK
        uuid family_id FK
        string title
        text description
        boolean is_shared
        boolean is_recurring
        string recurrence_rule
        timestamp starts_at
        timestamp ends_at
        timestamp created_at
        timestamp deleted_at
    }

    EVENT_PARTICIPANT {
        uuid id PK
        uuid event_id FK
        uuid user_id FK
    }

    LIST {
        uuid id PK
        uuid created_by FK
        uuid family_id FK
        string title
        string type
        boolean is_shared
        timestamp created_at
        timestamp deleted_at
    }

    TASK {
        uuid id PK
        uuid list_id FK
        uuid assigned_to FK
        string title
        string status
        timestamp due_at
        timestamp completed_at
        timestamp created_at
    }

    DOCUMENT {
        uuid id PK
        uuid user_id FK
        uuid family_id FK
        string title
        string file_url
        string file_type
        boolean is_shared
        date expires_at
        timestamp created_at
        timestamp deleted_at
    }

    NOTIFICATION {
        uuid id PK
        uuid user_id FK
        string type
        string title
        text body
        boolean is_read
        timestamp scheduled_at
        timestamp sent_at
    }

    MAINTENANCE {
        uuid id PK
        uuid family_id FK
        string title
        text description
        string category
        date last_done_at
        date next_due_at
        decimal cost
        timestamp created_at
        timestamp deleted_at
    }

    HEALTH_RECORD {
        uuid id PK
        uuid user_id FK
        string type
        string title
        text notes
        date date
        timestamp created_at
        timestamp deleted_at
    }

    MEDICATION {
        uuid id PK
        uuid user_id FK
        string name
        string dosage
        string frequency
        date start_date
        date end_date
        timestamp created_at
    }

    SMART_HOME_DEVICE {
        uuid id PK
        uuid family_id FK
        string name
        string type
        string integration
        string external_id
        boolean is_active
        timestamp created_at
    }

    FAMILY ||--o{ USER : "ha membri"
    USER ||--o{ MEMORY : "ha ricordi personali"
    FAMILY ||--o{ MEMORY : "ha ricordi condivisi"
    USER ||--o{ CONVERSATION : "avvia"
    CONVERSATION ||--o{ MESSAGE : "contiene"
    USER ||--o{ EXPENSE : "registra"
    FAMILY ||--o{ EXPENSE : "aggrega"
    USER ||--o{ BUDGET : "imposta"
    FAMILY ||--o{ BUDGET : "imposta"
    USER ||--o{ EVENT : "crea"
    FAMILY ||--o{ EVENT : "condivide"
    EVENT ||--o{ EVENT_PARTICIPANT : "ha partecipanti"
    USER ||--o{ EVENT_PARTICIPANT : "partecipa a"
    USER ||--o{ LIST : "crea"
    FAMILY ||--o{ LIST : "condivide"
    LIST ||--o{ TASK : "contiene"
    USER ||--o{ TASK : "è assegnato a"
    USER ||--o{ DOCUMENT : "archivia"
    FAMILY ||--o{ DOCUMENT : "condivide"
    FAMILY ||--o{ MAINTENANCE : "gestisce"
    USER ||--o{ HEALTH_RECORD : "ha"
    USER ||--o{ MEDICATION : "assume"
    USER ||--o{ NOTIFICATION : "riceve"
    FAMILY ||--o{ SMART_HOME_DEVICE : "possiede"
```

---

## Descrizione delle Entità

### USER
Rappresenta ogni persona registrata su Alfy. Ogni utente appartiene a esattamente una famiglia. Il campo `role` può essere `admin` o `member`. Il campo `deleted_at` permette il soft delete dell'account mantenendo lo storico dei dati associati.

### FAMILY
Il nucleo familiare. Contiene un `invite_code` generato automaticamente per invitare nuovi membri. Un utente che si registra senza codice crea una nuova famiglia da solo.

### MEMORY
È il sistema di memoria persistente di Alfy. Ogni ricordo ha uno `scope` (`personal` o `family`) e una coppia chiave-valore (`key`, `value`) che Alfy popola nel tempo. Esempi: `allergie: nichel`, `giorno_stipendio: 27`, `nome_animale: Luna`. Alfy legge questa tabella a ogni conversazione per contestualizzare le risposte.

### CONVERSATION / MESSAGE
Storico delle conversazioni con Alfy. Ogni conversazione è una sessione. I messaggi hanno un `role` (`user` o `assistant`) coerente con il formato delle API AI. Lo storico è usato per il contesto a breve termine all'interno di una sessione.

### EXPENSE
Ogni uscita o entrata registrata. Il campo `is_shared` distingue le spese personali da quelle familiari. Il soft delete (`deleted_at`) preserva lo storico finanziario.

### BUDGET
Limite di spesa impostato per categoria e periodo (`monthly`, `weekly`, `yearly`). Può essere personale o familiare.

### EVENT
Appuntamento o evento in calendario. Il campo `recurrence_rule` usa il formato iCal (es. `FREQ=WEEKLY;BYDAY=MO`) per gli eventi ricorrenti. Il soft delete preserva lo storico degli appuntamenti passati.

### EVENT_PARTICIPANT
Tabella di giunzione molti-a-molti tra EVENT e USER. Permette di associare più partecipanti a un evento condiviso.

### LIST
Contenitore di task. Il campo `type` può essere `shopping`, `todo`, `chores` o `custom`. Le liste possono essere personali o condivise.

### TASK
Singolo elemento di una lista. Il campo `status` può essere `todo`, `in_progress`, `done`. L'eliminazione dei task completati è definitiva dopo un periodo di grazia configurabile.

### DOCUMENT
File archiviato (foto, PDF, altri). Il campo `expires_at` permette ad Alfy di generare notifiche proattive sulle scadenze documentali. Il soft delete preserva lo storico.

### NOTIFICATION
Notifica generata dal sistema proattivo di Alfy. Il campo `scheduled_at` permette di pianificare notifiche future. Una volta letta (`is_read: true`) e trascorsa, la notifica viene eliminata definitivamente.

### MAINTENANCE
Registro degli interventi di manutenzione su casa e veicoli. Il campo `next_due_at` è usato dal sistema proattivo per generare promemoria. Il soft delete preserva lo storico.

### HEALTH_RECORD
Singolo evento sanitario (visita medica, esame, ricovero). Il campo `type` può essere `appointment`, `exam`, `prescription`, `other`. Sempre soft delete per ragioni di sensibilità dei dati.

### MEDICATION
Farmaco assunto regolarmente da un membro della famiglia. Alfy usa `frequency` e `start_date` / `end_date` per generare promemoria di assunzione o di riacquisto.

### SMART_HOME_DEVICE
Dispositivo smart collegato tramite integrazione esterna. Il campo `integration` indica il sistema usato (`home_assistant`, `google_home`, `matter`). Il campo `external_id` è l'identificativo del dispositivo nel sistema esterno.

---

## Politica di Eliminazione dei Dati

| Entità | Tipo di delete | Motivazione |
|--------|---------------|-------------|
| USER | Soft | Preserva lo storico dei dati associati |
| EXPENSE | Soft | Storico finanziario necessario |
| EVENT | Soft | Storico appuntamenti passati |
| DOCUMENT | Soft | Storico documentale |
| MAINTENANCE | Soft | Storico interventi |
| HEALTH_RECORD | Soft | Dati sensibili, sempre preservati |
| LIST | Soft | Può contenere task ancora attivi |
| TASK (completato) | Hard (dopo 30gg) | Dato operativo, non storico |
| NOTIFICATION (letta) | Hard | Dato effimero |
| MESSAGE | Hard (dopo 90gg) | Gestione contesto, non archivio |
| MEMORY | Hard | Aggiornamento continuo, no storico |

---

*Documento soggetto a revisione. L'ERD verrà aggiornato durante la fase di sviluppo al manifestarsi di nuove esigenze.*
