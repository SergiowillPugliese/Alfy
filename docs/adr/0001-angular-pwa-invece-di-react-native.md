# ADR 0001 — Frontend Angular PWA invece di React Native + Expo

**Data:** 2026-10-14
**Stato:** Accettato
**Sostituisce:** la scelta "React Native + Expo" in [Architettura](../alfy-architecture.md), sezione 2 (v0.1)

## Contesto

- In Fase 0 il frontend è stato impostato con React Native + Expo. La motivazione era "unico codebase per iOS, Android e Web" e la build iOS senza Mac tramite EAS.
- Alfy non verrà pubblicato sugli store: la distribuzione prevista è una PWA (web app installabile sulla home del telefono). È coerente con i vincoli del [PRD](../alfy-prd.md) (sezione 8): nessun Mac e budget limitato. La pubblicazione sull'App Store richiede comunque l'Apple Developer Program, a pagamento ogni anno.
- Senza app native, React Native sul web è solo uno strato di traduzione (componenti React Native → DOM) che non porta benefici al prodotto.
- Lo sviluppatore ha esperienza professionale su Angular e nessuna su React Native.
- Il costo del cambio oggi è minimo: il codice di Fase 0 è composto da tre schermate segnaposto e dal client Supabase.

## Decisione

Il frontend è un'applicazione **Angular distribuita come PWA**, con manifest e service worker. Il backend resta invariato: Supabase (PostgreSQL, Auth, Storage, Edge Functions).

## Alternative considerate

| Alternativa | Perché scartata |
|-------------|-----------------|
| React Native + Expo con target web/PWA | Il motivo della scelta, le app native, è venuto meno. Il supporto PWA è meno maturo (il service worker va configurato a mano). Stack nuovo per lo sviluppatore, senza benefici per il prodotto. |
| React Native + Expo con app native sugli store | Costo annuale dell'Apple Developer Program e processo di pubblicazione: non coerente con i vincoli del PRD. |
| Next.js / React web | Valido per una PWA, ma introduce un framework nuovo senza vantaggi rispetto ad Angular per questo progetto. |

## Conseguenze

**Positive**
- Supporto PWA integrato (`@angular/pwa`, `@angular/service-worker`): manifest, cache e consultazione offline richiesta dal PRD (sezione 7).
- Il frontend è terreno noto: le tecnologie nuove da imparare si concentrano sul backend (PostgreSQL, RLS, Edge Functions).
- Test su iPhone direttamente da Safari: niente Expo Go, niente tunnel.
- I link di autenticazione (conferma email, reset password) funzionano con il comportamento standard del client Supabase nel browser (`detectSessionInUrl`).

**Negative e rischi**
- **Notifiche push (F7):** Expo Notifications non è più disponibile. Serve Web Push: service worker, chiavi VAPID e invio da una Edge Function. Su iPhone funziona solo con la PWA installata sulla home (iOS 16.4+) e dopo il consenso dell'utente. **Da verificare prima della Fase 5**, perché le notifiche proattive sono un pilastro del prodotto.
- Le funzioni del dispositivo sono limitate a quelle esposte dalle API web. Fotocamera e file tramite input HTML bastano per F6.
- Il setup di Fase 0 va rifatto in Angular.
- Serve un hosting statico con HTTPS: il service worker non funziona su HTTP, tranne che su `localhost`.

**Invariato**
- Supabase, ERD, Edge Functions, integrazione con Claude API, funzionalità previste dalla roadmap.

## Da rivalutare se

- Le notifiche Web Push su iPhone si rivelano insufficienti per F7.
- Emerge un requisito nativo che le API web non coprono (es. widget, integrazioni di sistema).
