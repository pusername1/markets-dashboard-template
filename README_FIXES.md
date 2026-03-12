# Markets Dashboard (Static PWA) — Fixed Build

This build fixes:
- **DOM selector crash** when symbols contain special characters (e.g., `^SPX`, `AAPL.US`).
- **FRED path** (now relative) so it works under GitHub Pages subpaths.
- **Stooq CORS** via a safe fallback (`r.jina.ai`) if direct fetch is blocked.
- Added a **Reset** button to clear local settings.

Follow the same deployment steps as before (README in previous zip). Generated 2026-03-12.
