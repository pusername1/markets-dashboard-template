# Markets Dashboard (Static PWA)

Clean, fast, **grandma-deploy** market dashboard. Add instruments in 2–3 taps, compare GDP growth, and view tiles with deltas & sparklines. **No server needed**. Optional **FRED cache** via GitHub Actions keeps keys private.

## Data sources
- **Stooq** for EOD equities/indices/ETFs/commodities/FX (free, no key). Symbols like `AAPL.US`, `^SPX`, `CL.F`.  
- **World Bank** for GDP growth `NY.GDP.MKTP.KD.ZG` (annual, no key).  
- **FRED** via Action cache for series like `DGS5`, `SP500` (free key required, no keys in browser).  

## One‑minute deploy (GitHub Pages)
1. **Create a new GitHub repository** and upload the contents of this folder.
2. **Enable Actions write permission:** Settings → *Actions* → *General* → **Workflow permissions** → **Read and write**.
3. **Add FRED key (optional but recommended):** Settings → *Secrets and variables* → *Actions* → **New repository secret** → name `FRED_API_KEY` → paste your key.
4. **Enable Pages:** Settings → *Pages* → **Build and deployment** → *Deploy from branch* (branch: `main`, folder: `/ (root)`).
5. Wait for the Action and Pages to run (~1–2 min). Open the site at `https://<you>.github.io/<repo>/`.
6. On phone/desktop, tap **Install** to add it as an app.

## Usage
- **Add Apple:** click the search bar, type `app`, click **+ Add** on *Apple — AAPL.US*.
- **Compare GDP growth (US vs CN):** search `GDP_US_CN` → **+ Add**, then click **Compare** in the chart.
- **Replace tiles:** open tile → **Replace** → enter a symbol (e.g., `URTH.US`) or FRED series (e.g., `DGS5`).
- **Customize quick‑add chips:** **Customize** button → edit space‑separated symbols.

## Change which FRED series are cached
Edit `.github/workflows/fetch_fred.yml` → `FRED_SERIES: DGS5,SP500,IRLTLT01CZM156N` (comma‑separated). Commit. The Action rewrites `/data/fred/*.json` hourly.

## Notes
- If the FRED secret is missing, the Action will create empty JSON placeholders to avoid 404s; tiles will show **Load failed** until you add the key.
- This is a front‑end‑only PWA. For live intraday prices you will need a provider with a permissive API; EOD/Delayed sources work out of the box.

## License
MIT

---
*Generated on 2026-03-12*
