# Hueytown Rush Forecaster

Forecasts 15-minute sales, rushes, crew counts and break windows for Chick-fil-A Hueytown (#06123) from uploaded POS sales CSVs.

- **Scheduler** — daily forecast, peaks by daypart, shift builder, hour-by-hour counts.
- **On the Floor** — live status, tap-to-examine day timeline, line positions, game plan, Kitchen TV mode.

Single self-contained `index.html`. Without Firebase, data stays in the browser (localStorage). With Firebase configured, managers sign in with Google and every uploaded day is saved to Firestore under their account, synced live across devices and queued while offline.

Live: https://roudic.github.io/Bussiness-Forecaster/

## Deploying

`.github/workflows/pages.yml` publishes `index.html` to GitHub Pages on every push to `main`.
One-time setup: repo **Settings → Pages → Build and deployment → Source: GitHub Actions**.

## Cloud save and store teams (Firebase)

Project: `rush-forecaster`. Sign in with Google to save. The first person with data becomes the store **owner**; in **Store team** they add people by Gmail address as **Manager** (upload, edit positions and settings) or **View only** (kitchen tablet). Removing someone cuts access immediately.

Data: `stores/{id}` (name, ownerUid, managers[], viewers[]), `stores/{id}/days/{day}`, `stores/{id}/meta/config` (settings, positions). Each person's pre-team data in `users/{uid}` is moved into their store on first sign-in.

`firestore.rules` enforces all of it (team-only reads, owner/manager writes, owner-only deletes and team changes). Paste it into Firebase console → Firestore Database → Rules → Publish. Until the team rules are published the app falls back to each account's own `users/{uid}` space.
