# Index

Lightweight JSON for UIs. **Generated - do not hand-edit.**

| File | Purpose |
|------|---------|
| `manifest.json` | Totals + category list |
| `categories/<slug>.json` | Card summaries for one category (id, title, tags, path) |
| `by-month/YYYY-MM.json` | Cards published that month |

UI flow: load `manifest.json` → open one category shard → fetch a single checklist `.md` when the user expands a card.
