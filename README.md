# Hueytown Rush Forecaster

Forecasts 15-minute sales, rushes, crew counts and break windows for Chick-fil-A Hueytown (#06123) from uploaded POS sales CSVs.

- **Scheduler** — daily forecast, peaks by daypart, shift builder, hour-by-hour counts.
- **On the Floor** — live status, tap-to-examine day timeline, line positions, game plan, Kitchen TV mode.

Single self-contained `index.html`. Data stays in the browser (localStorage); nothing is uploaded anywhere.

Live: https://roudic.github.io/Bussiness-Forecaster/

## Deploying

`.github/workflows/pages.yml` publishes `index.html` to GitHub Pages on every push to `main`.
One-time setup: repo **Settings → Pages → Build and deployment → Source: GitHub Actions**.
