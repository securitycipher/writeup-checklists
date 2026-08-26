# Index

Lightweight JSON for UIs. **Generated - do not hand-edit.**

| File | Purpose |
|------|---------|
| `catalog.json` | All card summaries (primary feed for the live UI) |
| `manifest.json` | Totals + category list |
| `categories/<slug>.json` | Card summaries for one category |
| `by-month/YYYY-MM.json` | Cards published that month |

UI flow: load `catalog.json` → fetch a single checklist `.md` when the user opens a card.
