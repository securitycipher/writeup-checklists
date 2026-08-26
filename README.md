# Writeup Checklists

> Real bug bounty writeups → copy-paste security checklists.

Every week hunters publish Medium / InfoSecWriteups posts about IDOR, race conditions, auth bypass, and business logic. Most of them die in your reading list.

**This repo turns those writeups into actionable checklist cards** you can run on your next target: quick test, steps, commands, tools, and a link back to the original article.

Built by [SecurityCipher](https://securitycipher.com) · sibling of [security-checklists](https://github.com/securitycipher/security-checklists)

---

## Why this exists

| Generic checklists | Writeup checklists |
|---|---|
| "Test for IDOR" | "Swap `user_id` on password-reset → mass ATO (from a real \$ bounty writeup)" |
| Abstract OWASP bullets | Exact steps + commands extracted from hunter writeups |
| Rarely updated | Fed from daily bounty writeups |

Steal the technique. Credit the author. Ship the finding.

---

## Quick peek

```text
Category: Broken Access Control / IDOR
Quick test: Change User_Id on password reset without auth
Steps: 6 · Commands: Burp Repeater · Source: writeup
```

Browse by category under [`checklists/`](./checklists). Each card is **one Markdown file** - not a giant dump.

---

## Repo layout (built for scale)

Do **not** store everything in one `checklists.json`. At 10k–100k+ cards that file becomes unreadable, unreviewable, and unusable in any UI.

```text
writeup-checklists/
├── README.md
├── LICENSE
├── schema/
│   └── checklist.schema.json      # shape of one card
├── checklists/                    # SOURCE OF TRUTH (one file per card)
│   ├── broken-access-control/
│   │   └── 9d4d4e15e022.md
│   ├── authentication/
│   │   └── dc88ae0abf32.md
│   ├── race-condition/
│   ├── injection/
│   └── ...
├── index/                         # LIGHTWEIGHT indexes for UIs / search
│   ├── manifest.json              # counts, category list, last updated
│   ├── categories/
│   │   └── broken-access-control.json   # id, title, tags, path only
│   └── by-month/
│       └── 2026-08.json
└── examples/
    └── sample-checklist.md
```

### Rules that keep this manageable

1. **One checklist = one Markdown file** (YAML frontmatter + body).
2. **Filename = short fingerprint** (hash of canonical URL) so renames/dedupe stay stable.
3. **Folder = category slug** (`broken-access-control`, `race-condition`, …).
4. **`index/` is generated**, never hand-edited. Rebuild with a script after adds.
5. **UI never loads every card.** Load `index/manifest.json` → one category shard → fetch a single `.md` on open.
6. **Skipped / junk writeups stay out of git.** Only curated, actionable cards land here.

---

## Checklist card format

```markdown
---
id: 9d4d4e15e022
title: "I Changed One User_Id and the API Said Sure"
source_url: https://infosecwriteups.com/...
author: Rajdip Chavan
publication_date: 2026-08-24
category: broken-access-control
content_type: vuln_writeup
steps_source: extracted
tags: [idor, password-reset, ato, bug-bounty]
tools: [Burp Repeater]
quick_test: "Test password reset for IDOR by swapping User_Id."
---

## Use case

Password reset accepted another user's id without auth checks...

## Steps to test

1. ...
2. ...

## Commands

    POST /api/password-reset HTTP/1.1
    Host: target.example
    {"user_id":"VICTIM_ID"}
```

Full JSON Schema: [`schema/checklist.schema.json`](./schema/checklist.schema.json)  
Full example: [`examples/sample-checklist.md`](./examples/sample-checklist.md)

---

## How the UI should consume this (even at 100k+ cards)

```text
┌─────────────┐     ┌──────────────────┐     ┌─────────────────┐
│ manifest.json│ ──► │ category shard   │ ──► │ single .md card │
│ (~few KB)    │     │ (titles only)    │     │ (lazy on open)  │
└─────────────┘     └──────────────────┘     └─────────────────┘
```

- **List view:** virtualized table/list over the category JSON (thousands of rows, fine).
- **Search:** build a tiny search index in CI (`id`, `title`, `tags`, `category`) - do not grep every Markdown file in the browser.
- **Filters:** category + tags + month shards under `index/by-month/`.
- **WordPress / SecurityCipher:** sync only the index + requested cards; never embed the whole repo in a page.

If you ever outgrow git as a store (multi-hundred-thousand cards), keep Markdown as export/source and add a read replica (SQLite / Typesense). Until then, **sharded indexes + one-file-per-card is enough**.

---

## What we will / will not store

| In repo | Out of repo |
|---|---|
| Actionable steps + commands | Full Medium article text |
| Attribution + source URL | Paywalled content pasted in |
| Category, tags, tools | Raw scrape HTML / caches |
| Curated cards only | Noise, journey posts, dead links |

Ethics: these are **testing checklists for authorized targets** (bug bounty / pentest scope). Not exploit packs for random sites.

---

## Status

**73 checklist cards** in `22` categories (updated 2026-08-26).

Browse [`checklists/`](./checklists) or load [`index/manifest.json`](./index/manifest.json) for UI integrations.

Coming next:

- [x] Seed first batch from Daily Bug Bounty Writeups extract
- [ ] Index builder CI
- [ ] Site page on [securitycipher.com](https://securitycipher.com) that reads `index/`

---

## Related

- Live checklists UI: [securitycipher.com/security-checklists](https://securitycipher.com/security-checklists/)
- Daily bounty writeups: [securitycipher.com/bounty-writeups](https://securitycipher.com/bounty-writeups/)
- Interactive assessments: [github.com/securitycipher/security-checklists](https://github.com/securitycipher/security-checklists)

---

## License

Content in this repo is for educational / authorized security testing.  
Original writeup copyright stays with each author - we only store derived checklist steps and link back.

If you are an author and want a card removed or corrected, open an issue.
