# Hueytown Rush Forecaster

Forecasts 15-minute sales, rushes, crew counts and break windows for Chick-fil-A Hueytown (#06123) from uploaded POS sales CSVs.

- **Scheduler** — daily forecast, peaks by daypart, shift builder, hour-by-hour counts.
- **On the Floor** — live status, tap-to-examine day timeline, line positions, game plan, Kitchen TV mode.

Single self-contained `index.html`. Without Firebase, data stays in the browser (localStorage). With Firebase configured, managers sign in with Google and every uploaded day is saved to Firestore under their account, synced live across devices and queued while offline.

Live: https://roudic.github.io/Bussiness-Forecaster/

## Deploying

`.github/workflows/pages.yml` publishes `index.html` to GitHub Pages on every push to `main`.
One-time setup: repo **Settings → Pages → Build and deployment → Source: GitHub Actions**.

## Cloud save (Firebase)

1. Create a project at https://console.firebase.google.com and add a **Web app**. Copy its config object.
2. Paste it into `const FIREBASE_CONFIG=null;` near the bottom of `index.html`.
3. **Authentication → Sign-in method:** enable **Google**. **Authentication → Settings → Authorized domains:** add `roudic.github.io`.
4. **Firestore Database:** create it (production mode), then paste `firestore.rules` into the **Rules** tab and publish.

Data lives at `users/{uid}/days/{day}` (one doc per business day) and `users/{uid}` (settings). The web config is public by design; the rules are what keep each account's sales private.
