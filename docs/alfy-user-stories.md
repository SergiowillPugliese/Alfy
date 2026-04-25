# User Stories — Alfy: Il Maggiordomo Digitale

**Versione:** 0.1 (Draft)
**Data:** Marzo 2026
**Autore:** Sergio
**Stato:** In revisione

---

## Legenda Utenti

- **Admin** — membro della famiglia con ruolo di amministratore (es. genitore organizzatore)
- **Membro** — membro della famiglia con accesso standard (es. partner, figlio maggiorenne)
- **Ospite Tablet** — utente che accede tramite l'Hub Familiare (tablet condiviso)

---

## F1 — Core AI: Alfy

| ID | Storia |
|----|--------|
| US-01 | Come **utente**, voglio parlare con Alfy in linguaggio naturale, così da non dover imparare dove si trovano le funzioni nell'app. |
| US-02 | Come **utente**, voglio che Alfy ricordi le informazioni che gli ho fornito nelle conversazioni passate, così da non doverle ripetere ogni volta. |
| US-03 | Come **utente**, voglio che Alfy capisca richieste ambigue e mi chieda chiarimenti quando necessario, così da ottenere sempre il risultato corretto. |
| US-04 | Come **utente**, voglio che Alfy confermi le azioni prima di eseguirle quando queste sono irreversibili (es. eliminazione di un documento), così da evitare errori accidentali. |
| US-05 | Come **utente**, voglio che Alfy mi risponda con un tono caldo e personale, così da percepire l'esperienza come quella di un vero maggiordomo e non di un bot. |
| US-06 | Come **admin**, voglio poter dire ad Alfy informazioni generali sulla mia famiglia (nomi, allergie, preferenze), così che le usi automaticamente nel tempo. |

---

## F2 — Gestione Utenti e Famiglia

| ID | Storia |
|----|--------|
| US-07 | Come **admin**, voglio creare un nucleo familiare e invitare altri membri tramite email o codice, così da condividere Alfy con la mia famiglia. |
| US-08 | Come **admin**, voglio assegnare ruoli ai membri della famiglia (admin, membro), così da controllare chi può modificare le impostazioni condivise. |
| US-09 | Come **membro**, voglio avere un profilo personale con dati privati che gli altri membri non possono vedere, così da mantenere la mia privacy anche all'interno della famiglia. |
| US-10 | Come **utente**, voglio poter scegliere se un contenuto (spesa, appuntamento, documento) è personale o condiviso con la famiglia, così da avere controllo sulla visibilità. |
| US-11 | Come **utente**, voglio poter modificare il mio profilo (nome, foto, preferenze), così da personalizzare la mia esperienza con Alfy. |
| US-12 | Come **admin**, voglio poter rimuovere un membro dalla famiglia, così da gestire cambiamenti nel nucleo familiare. |

---

## F3 — Spese e Budget

| ID | Storia |
|----|--------|
| US-13 | Come **utente**, voglio dire ad Alfy "ho speso 45€ al supermercato oggi" e vederla registrata automaticamente, così da tracciare le spese senza aprire form. |
| US-14 | Come **utente**, voglio impostare un budget mensile per categoria (es. alimentari, svago), così da ricevere un avviso quando mi sto avvicinando al limite. |
| US-15 | Come **utente**, voglio chiedere ad Alfy "quanto ho speso questo mese in ristoranti?" e ricevere un riepilogo immediato, così da monitorare le mie abitudini. |
| US-16 | Come **admin**, voglio vedere le spese aggregate della famiglia divise per membro, così da capire come viene distribuito il budget familiare. |
| US-17 | Come **utente**, voglio poter assegnare una spesa alla famiglia o tenerla personale, così da separare le uscite condivise da quelle private. |
| US-18 | Come **utente**, voglio ricevere un riepilogo mensile delle spese da Alfy senza doverlo chiedere, così da avere sempre una visione chiara delle mie finanze. |

---

## F4 — Agenda e Appuntamenti

| ID | Storia |
|----|--------|
| US-19 | Come **utente**, voglio dire ad Alfy "aggiungi visita dal dentista giovedì alle 10" e trovarlo nel mio calendario, così da gestire gli appuntamenti in modo rapido. |
| US-20 | Come **utente**, voglio ricevere un promemoria da Alfy il giorno prima di un appuntamento importante, così da non dimenticarlo. |
| US-21 | Come **admin**, voglio creare eventi condivisi visibili a tutti i membri della famiglia, così da coordinare gli impegni comuni. |
| US-22 | Come **utente**, voglio chiedere ad Alfy "cosa ho in agenda questa settimana?" e ricevere un riepilogo ordinato, così da pianificare la mia settimana facilmente. |
| US-23 | Come **utente**, voglio impostare eventi ricorrenti (es. riunione ogni lunedì), così da non doverli reinserire ogni volta. |
| US-24 | Come **utente**, voglio che Alfy sincronizzi gli appuntamenti con Google Calendar, così da avere tutto in un unico posto. |

---

## F5 — Liste e Task

| ID | Storia |
|----|--------|
| US-25 | Come **utente**, voglio dire ad Alfy "aggiungi latte e pane alla lista della spesa", così da aggiornare la lista senza aprire l'app manualmente. |
| US-26 | Come **membro**, voglio vedere la lista della spesa condivisa dalla famiglia, così da poter fare la spesa anche quando sono io a passare dal supermercato. |
| US-27 | Come **admin**, voglio assegnare un task a un altro membro della famiglia, così da delegare le responsabilità domestiche. |
| US-28 | Come **utente**, voglio marcare un task come completato tramite chat con Alfy, così da aggiornare la lista senza navigare l'interfaccia. |
| US-29 | Come **utente**, voglio avere liste diverse per contesti diversi (spesa, lavori di casa, cose da fare), così da tenere organizzate le attività per categoria. |
| US-30 | Come **membro**, voglio ricevere una notifica quando mi viene assegnato un task, così da essere avvisato tempestivamente. |

---

## F6 — Documenti e Ricevute

| ID | Storia |
|----|--------|
| US-31 | Come **utente**, voglio fotografare una ricevuta e dirlo ad Alfy, così da archiviarla senza doverla catalogare manualmente. |
| US-32 | Come **utente**, voglio chiedere ad Alfy "dove ho messo la garanzia del frigo?", così da trovare un documento senza cercare tra le cartelle. |
| US-33 | Come **admin**, voglio archiviare documenti importanti della famiglia (contratti, documenti d'identità), così da averli sempre accessibili e in sicurezza. |
| US-34 | Come **utente**, voglio che Alfy mi avvisi quando la scadenza di un documento si avvicina (es. carta d'identità in scadenza), così da rinnovarla in tempo. |
| US-35 | Come **utente**, voglio poter decidere se un documento è privato o condiviso con la famiglia, così da mantenere il controllo sulla riservatezza. |

---

## F7 — Notifiche Proattive

| ID | Storia |
|----|--------|
| US-36 | Come **utente**, voglio ricevere una notifica da Alfy quando si avvicina la scadenza di una bolletta, così da non dimenticare di pagarla. |
| US-37 | Come **utente**, voglio che Alfy mi ricordi i compleanni dei membri della famiglia con qualche giorno di anticipo, così da avere il tempo di organizzarmi. |
| US-38 | Come **utente**, voglio ricevere un buongiorno da Alfy con il riepilogo degli impegni del giorno, così da iniziare la giornata con una visione chiara. |
| US-39 | Come **admin**, voglio configurare quali tipi di notifiche voglio ricevere e con quale anticipo, così da personalizzare il comportamento proattivo di Alfy. |
| US-40 | Come **membro**, voglio ricevere solo le notifiche che mi riguardano direttamente, così da non essere sommerso da avvisi familiari irrilevanti per me. |

---

## F8 — Casa e Manutenzioni

| ID | Storia |
|----|--------|
| US-41 | Come **admin**, voglio registrare tramite Alfy la data dell'ultima revisione della caldaia, così da sapere quando programmare la prossima. |
| US-42 | Come **utente**, voglio chiedere ad Alfy "quando scade il bollo della macchina?", così da trovare subito l'informazione senza cercare tra i documenti. |
| US-43 | Come **admin**, voglio tenere un registro di tutti i lavori di manutenzione fatti in casa con data e costo, così da avere uno storico completo. |
| US-44 | Come **utente**, voglio ricevere un avviso da Alfy quando si avvicina una manutenzione programmata, così da organizzarmi per tempo. |

---

## F9 — Salute e Benessere

| ID | Storia |
|----|--------|
| US-45 | Come **utente**, voglio registrare gli appuntamenti medici dei membri della famiglia tramite Alfy, così da averli in un unico posto separato dall'agenda generale. |
| US-46 | Come **admin**, voglio tenere un registro dei farmaci che i membri della famiglia assumono regolarmente, così da non dimenticare di acquistarli o somministrarli. |
| US-47 | Come **utente**, voglio che Alfy mi ricordi di prendere un farmaco all'orario stabilito, così da non dimenticarlo. |
| US-48 | Come **admin**, voglio poter registrare allergie e condizioni mediche dei membri della famiglia, così che Alfy le conosca e le tenga in considerazione. |
| US-49 | Come **utente**, voglio che i dati sanitari siano strettamente privati e non visibili ad altri membri senza consenso esplicito, così da tutelare la mia riservatezza. |

---

## F10 — Hub Familiare (Modalità Tablet)

| ID | Storia |
|----|--------|
| US-50 | Come **ospite tablet**, voglio vedere in tempo reale gli impegni del giorno della famiglia, così da essere aggiornato senza aprire l'app personale. |
| US-51 | Come **ospite tablet**, voglio poter aggiungere un elemento alla lista della spesa condivisa direttamente dal tablet all'ingresso, così da farlo mentre ci penso. |
| US-52 | Come **ospite tablet**, voglio poter parlare con Alfy dal tablet usando l'utenza famiglia, così da fare richieste rapide senza autenticarmi con il mio profilo personale. |
| US-53 | Come **admin**, voglio configurare cosa mostra l'Hub Familiare (eventi, liste, meteo, notifiche), così da personalizzare la vista condivisa. |

---

## F11 — Smart Home (Integrazione Esterna)

| ID | Storia |
|----|--------|
| US-54 | Come **utente**, voglio dire ad Alfy "spegni le luci del salotto", così da controllare i dispositivi smart senza usare un'app separata. |
| US-55 | Come **utente**, voglio dire ad Alfy "accendi la lavatrice tra un'ora", così da programmare gli elettrodomestici smart tramite conversazione. |
| US-56 | Come **admin**, voglio collegare Alfy al mio sistema Home Assistant, così da usare Alfy come punto unico di controllo della casa. |
| US-57 | Come **utente**, voglio chiedere ad Alfy "le luci di casa sono accese?", così da avere una panoramica dello stato dei dispositivi senza aprire altre app. |

---

*Documento soggetto a revisione. Le user stories verranno dettagliate con criteri di accettazione nella fase di sviluppo di ciascuna funzionalità.*
