# Feature — Fase 0: Setup e Fondamenta

## Panoramica

Setup iniziale del progetto Alfy: ambiente di sviluppo, navigazione, connessione a Supabase.

## Componenti

### Navigazione (Expo Router)
- **Root layout** (`app/_layout.tsx`): Stack navigator, avvolge tutta l'app
- **Tab layout** (`app/(tabs)/_layout.tsx`): Tab bar con 3 tab (Home, Alfy, Profilo)
- **Schermate placeholder**: `index.tsx`, `chat.tsx`, `profile.tsx`

### Supabase Client
- **Client** (`lib/supabase.ts`): singleton con AsyncStorage per persistenza sessione
- **Variabili d'ambiente** (`.env`): `EXPO_PUBLIC_SUPABASE_URL`, `EXPO_PUBLIC_SUPABASE_KEY`

## Decisioni non ovvie

| Decisione | Motivazione |
|-----------|-------------|
| Flat structure (no monorepo) | Complessità prematura per singolo sviluppatore |
| `expo-router/entry` come main | Expo Router gestisce il proprio entry point, non serve `registerRootComponent` manuale |
| `detectSessionInUrl: false` | In React Native il token OAuth non arriva via URL come nel browser |
| `@expo/ngrok` installato | Per tunnel mode quando PC e telefono sono su reti diverse |

## Dipendenze aggiunte

| Package | Versione | Scopo |
|---------|----------|-------|
| `expo-router` | ~6.0 | File-based routing |
| `react-native-screens` | ~4.16 | Navigazione nativa ottimizzata |
| `react-native-safe-area-context` | ~5.6 | Safe area (notch, barra di stato) |
| `react-native-gesture-handler` | ~2.28 | Gesture (swipe, pan) |
| `@expo/vector-icons` | ^15.0 | Icone nella tab bar |
| `expo-constants` | ~18.0 | Costanti di sistema Expo |
| `expo-linking` | ~8.0 | Deep linking |
| `@supabase/supabase-js` | latest | Client Supabase |
| `@react-native-async-storage/async-storage` | latest | Storage locale per sessione |
| `@expo/ngrok` | ^4.1 | Tunnel per test remoto |
