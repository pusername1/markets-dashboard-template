# Markets v2 — Charts Only (Static PWA)

Minimal, reliable market **charts** stacked vertically. No tiles. You pick a **provider** and a **series ID**, the app draws the chart. Optional compare, normalization (base=100), moving average, and global range chips. All settings persist in your browser (import/export JSON).

## Supported providers
- **ECB (SDMX 2.1)** — use a series key like `EXR/D.USD.EUR.SP00.A` (USD per EUR, daily reference). Endpoint: `.../service/data/<key>?format=SDMX-CSV`.  Docs: https://data.ecb.europa.eu/help/api/data 
- **FRED** — any series ID (e.g., `SP500`, `DGS10`, `WTISPLC`). Requires your personal API key; paste it in **Settings** (kept in localStorage). Endpoint: `fred/series/observations` `file_type=json`.  Docs: https://fred.stlouisfed.org/docs/api/fred/ 
- **World Bank** — `ISO3:INDICATOR` like `CZE:NY.GDP.MKTP.KD.ZG`. Endpoint: `api.worldbank.org/v2/country/<iso3>/indicator/<ind>?format=json&per_page=20000`.  Docs: https://datahelpdesk.worldbank.org/knowledgebase/articles/889392-about-the-indicators-api-documentation 
- **Stooq** — daily EOD CSV for `AAPL.US`, `^SPX`, etc. Endpoint: `https://stooq.com/q/d/l/?s=<symbol>&i=d`. 
- **Yahoo Finance** — best‑effort. Browsers may block direct calls (CORS). Use the optional **serverless cache** (GitHub Action) to fetch to `/data/yahoo/*.json`.

> References: ECB SDMX endpoint and EXR keys; FRED series/observations; World Bank v2 indicators; Yahoo CORS caveat. See docs above.

## Quick start (2–3 minutes)

1. **Create (or open) a GitHub repo** (empty is fine).
2. Add these files at the **repo root**:
   - `index.html` (this app)
   - `service-worker.js` (optional, for offline caching)
   - `.nojekyll` (empty file, disables Jekyll on Pages)
   - `data/yahoo/.gitkeep` (optional; only if you want Yahoo cache)
   - `.github/workflows/fetch_yahoo.yml` (optional)

3. **Enable GitHub Pages** → Settings → Pages → Build & deployment → *Deploy from a branch* → Branch: `main` → Folder: `/ (root)`.
4. Open your site (URL pattern): `https://<user>.github.io/<repo>/`.
5. In the app, **Settings** → paste your **FRED API key** (kept locally). Add your first chart:
   - Provider: *ECB* → ID: `EXR/D.USD.EUR.SP00.A` → **Add**.
   - Compare (optional), Normalize (base date), Moving Avg, Range chips.

### Optional: Yahoo cache via GitHub Actions
1. Ensure path `data/yahoo/` exists (the `.gitkeep` placeholder does that).
2. Open **Actions** → **Fetch Yahoo** → **Run workflow** and enter symbols (e.g., `AAPL,MSFT,SPY`).
3. The Action writes `/data/yahoo/<SYMBOL>.json`. The app prefers the cached file; if missing, it tries Yahoo live (may be CORS‑blocked).

## Notes
- **ECB**: Use SDMX **series keys** (e.g., EXR frequency/currency/type). The app parses `SDMX-CSV` columns `TIME_PERIOD` & `OBS_VALUE`.
- **World Bank**: Responses are paginated by default. `per_page=20000` fetches full history in one call.
- **Persistence**: Everything is saved to `localStorage` under `v2cfg`. Use **Export/Import JSON** to migrate configs.
- **Security**: FRED key remains in your browser only (not committed anywhere). Yahoo cache (if used) stores **prices only** in your repo.

## Troubleshooting
- **ECB chart empty**: Double‑check the series key and that CSV opens directly in your browser.
- **FRED error**: Paste a valid API key in Settings. Try `SP500` as a quick test.
- **World Bank**: Ensure `ISO3:INDICATOR` format (e.g., `USA:NY.GDP.MKTP.CD`).
- **Yahoo**: Prefer the **cache** workflow to avoid CORS.

---

© You. MIT/Apache‑2.0 as you prefer.
