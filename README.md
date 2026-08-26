# Writeup Checklists

<p align="center">
  <strong>Bug bounty writeups → copy-paste testing checklists</strong><br/>
  <a href="https://securitycipher.com/writeup-checklists/">Open the live UI</a>
  ·
  <a href="https://securitycipher.com">SecurityCipher</a>
  ·
  <a href="https://github.com/securitycipher/security-checklists">Security Checklists</a>
</p>

---

Real hunters publish writeups every day. This repo turns those findings into short, actionable checklist cards you can reuse on your next in-scope target.

Each card has a quick test, step-by-step checks, commands when available, tools, and a link back to the original writeup.

### Live browser

**→ [securitycipher.com/writeup-checklists](https://securitycipher.com/writeup-checklists/)**

Search, filter by category, expand a card, copy the markdown.

<p align="center">
  <a href="https://securitycipher.com/writeup-checklists/">
    <img src="./docs/writeup-checklists-ui.png" alt="SecurityCipher Writeup Checklists UI - search, filter, and open a card with steps and commands" width="100%" />
  </a>
  <br/>
  <em>Live Writeup Explorer on SecurityCipher - 349 cards, search + category filters, steps and commands side by side.</em>
</p>

---

## Features (live UI)

| Feature | What it does |
|---------|----------------|
| **Search** | Find cards by vuln class, title, author, or tags |
| **Category filters** | Narrow to IDOR, XSS, SSRF, RCE, auth, and more |
| **Unread / Favorites** | Personal queue saved in your browser |
| **Split view** | List on the left, full checklist on the right |
| **Use case + steps** | Quick test intent, then numbered reproduction steps |
| **Commands** | Copy request / payload snippets when the writeup had them |
| **Original writeup** | One click back to the source post |
| **GitHub-backed** | Cards ship from this repo (`index/catalog.json` + Markdown bodies) |

---

## At a glance

<!-- BEGIN STATS -->
| | |
|---|---|
| Checklist cards | **349** |
| Categories | **30** |
| Last updated | **26 Aug 2026** |
| Format | One Markdown file per card |
| Live UI | [securitycipher.com/writeup-checklists](https://securitycipher.com/writeup-checklists/) |
<!-- END STATS -->

Growing as new writeups are curated. Expect this number to keep climbing.

---

## Categories

<!-- BEGIN CATEGORIES -->
| Category | Cards |
|----------|------:|
| [API Security](./checklists/api-security/) | 18 |
| [Authentication / Password Reset](./checklists/authentication/) | 38 |
| [Broken Access Control / IDOR](./checklists/broken-access-control/) | 53 |
| [Business Logic](./checklists/business-logic/) | 31 |
| [Cache Poisoning](./checklists/cache-poisoning/) | 2 |
| [CORS Misconfiguration](./checklists/cors/) | 3 |
| [Denial of Service](./checklists/denial-of-service/) | 3 |
| [File Upload / Stored XSS](./checklists/file-upload-stored-xss/) | 3 |
| [General Web Security](./checklists/general-web/) | 12 |
| [Host Header Injection](./checklists/host-header-injection/) | 2 |
| [HTTP Request Smuggling](./checklists/http-request-smuggling/) | 1 |
| [IDOR](./checklists/idor/) | 8 |
| [Information Disclosure](./checklists/information-disclosure/) | 12 |
| [Injection (SQL / NoSQL)](./checklists/injection/) | 28 |
| [Mass Assignment](./checklists/mass-assignment/) | 3 |
| [Methodology / Tooling](./checklists/methodology-tooling/) | 8 |
| [Mobile / JS Bridge](./checklists/mobile/) | 5 |
| [OAuth / SSO](./checklists/oauth-sso/) | 11 |
| [Open Redirect / CSRF](./checklists/open-redirect-csrf/) | 3 |
| [Path Traversal / Arbitrary File Read](./checklists/path-traversal/) | 5 |
| [Privilege Escalation](./checklists/privilege-escalation/) | 12 |
| [Prompt Injection / AI Agent](./checklists/prompt-injection/) | 1 |
| [Race Condition](./checklists/race-condition/) | 6 |
| [RCE / Code Execution](./checklists/rce/) | 23 |
| [Recon / OSINT](./checklists/recon-osint/) | 22 |
| [SSRF](./checklists/ssrf/) | 10 |
| [SSRF, Host Header Injection](./checklists/ssrf-host-header-injection/) | 1 |
| [Subdomain Takeover](./checklists/subdomain-takeover/) | 3 |
| [XSS](./checklists/xss/) | 19 |
| [XXE / XML](./checklists/xxe/) | 3 |
<!-- END CATEGORIES -->

---

## How the data is organized

```text
checklists/
  broken-access-control/
    <id>.md          ← one checklist card
  authentication/
    <id>.md
  ...

docs/
  writeup-checklists-ui.png   ← live UI screenshot

index/
  catalog.json       ← all card summaries (for the live UI)
  categories/        ← per-category summaries
  manifest.json      ← totals + category list
```

- **Source of truth:** Markdown files under `checklists/`
- **Each file:** frontmatter (title, author, tags, quick test) + steps + commands
- **Indexes:** lightweight JSON for search/UI - not a dump of full article text

---

## What you will find (and what you will not)

**Included**
- Practical test steps from public writeups
- Commands / request snippets when the writeup has them
- Author credit + link to the original post

**Not included**
- Full Medium article text
- Paywalled content
- Junk / journey posts with no actionable test

For authorized testing only (bug bounty / pentest scope).

---

## Related

- [Live Writeup Checklists UI](https://securitycipher.com/writeup-checklists/)
- [Daily Bug Bounty Writeups](https://securitycipher.com/bounty-writeups/)
- [Interactive Security Checklists](https://securitycipher.com/security-checklists/)
- [security-checklists on GitHub](https://github.com/securitycipher/security-checklists)

---

## License

MIT for the repo tooling/layout. Derived checklist wording links back to original authors - we do not republish full writeups.

Want a card fixed or removed? Open an issue.
