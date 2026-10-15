# Piano — Fase 0 (bis): Migrazione ad Angular PWA

**Data:** 2026-10-14
**Stato:** in corso
**Fase Roadmap:** 0
**Decisione di riferimento:** [ADR 0001](../adr/0001-angular-pwa-invece-di-react-native.md)

## Obiettivo

Sostituire il prototipo React Native + Expo con un'app Angular installabile come PWA, connessa a Supabase e testata su iPhone.

## Decisioni

| Decisione | Scelta | Motivo |
|-----------|--------|--------|
| Repository | Stesso repo; il prototipo Expo viene rimosso in un commit dedicato | La storia (prototipo → ADR → Angular) documenta la decisione. Il prototipo resta recuperabile dal commit `10832a2`. |
| Configurazione Supabase | `src/environments/environment.ts` committato con URL e publishable key reali | Sono valori pubblici per costruzione: finiscono nel bundle della PWA pubblicata. La protezione dei dati è la RLS, non la chiave. In Fase 1 `environment.development.ts` punterà al Supabase locale della CLI (`fileReplacements`). |
| SSR/SSG | No | Hosting statico senza server; la sessione Supabase vive nel `localStorage`, che lato server non esiste. |
| Change detection | Zoneless, componenti standalone, signal | Default dei progetti nuovi: nessun codice legacy da convertire. |
| Test runner | Vitest | Default di Angular CLI 22. |
| Stili | SCSS | Proposta, modificabile al momento di `ng new`. |
| Client Supabase | `InjectionToken` con factory in `src/app/core/supabase.ts` | Nessuna classe wrapper con una sola proprietà; nei test si sostituisce con un provider. |

## Passi

- [x] Commit della documentazione (ADR 0001)
- [x] Rimuovere il prototipo Expo (commit dedicato)
- [x] `ng new` in una cartella temporanea, poi spostamento nel repo (README esistente mantenuto, `.gitignore` unito) — commit con il solo codice generato. La cartella `.vscode/` generata non è stata copiata.
- [x] Eliminare il vecchio `node_modules` di Expo e lanciare `npm install` — `package-lock.json` in un commit dedicato; `ng build` dello scaffold verificato
- [x] `ng add @angular/pwa` — commit separato. Prima, `allowScripts` in `package.json` approva gli install script delle dipendenze di `@angular/build` (esbuild, lmdb, msgpackr-extract, @parcel/watcher). Manifest e icone sono ancora quelli generati (nome `alfy`, logo Angular)
- [ ] Client Supabase ed environments — commit
- [ ] Schermata di benvenuto al posto del template di default
- [ ] Verifica: `ng build` e `ng test`
- [ ] Aggiornare README (prerequisiti, setup, struttura) e roadmap
- [ ] Hosting statico HTTPS e test su iPhone (Safari + installazione sulla home)
- [ ] Spike Web Push: verificare che una notifica di test arrivi sull'iPhone con la PWA installata

## Note

- Codice generato dalla CLI e codice scritto a mano vanno in commit separati: così si distingue a colpo d'occhio cosa è stato scritto e cosa è stato prodotto dagli strumenti.
