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

Prefer clicking over cloning?

**→ [securitycipher.com/writeup-checklists](https://securitycipher.com/writeup-checklists/)**

Search, filter by category, expand a card, copy the markdown.

---

## At a glance

| | |
|---|---|
| Checklist cards | **73** |
| Categories | **22** |
| Last updated | **26 Aug 2026** |
| Format | One Markdown file per card |
| Live UI | [securitycipher.com/writeup-checklists](https://securitycipher.com/writeup-checklists/) |

Growing as new writeups are curated. Expect this number to keep climbing.

---

## Categories

| Category | Cards |
|----------|------:|
| [Broken Access Control / IDOR](./checklists/broken-access-control/) | 10 |
| [Authentication / Password Reset](./checklists/authentication/) | 9 |
| [Injection (SQL / NoSQL)](./checklists/injection/) | 7 |
| [General Web Security](./checklists/general-web/) | 7 |
| [Methodology / Tooling](./checklists/methodology-tooling/) | 7 |
| [Mobile / JS Bridge](./checklists/mobile/) | 4 |
| [RCE / Code Execution](./checklists/rce/) | 4 |
| [Recon / OSINT](./checklists/recon-osint/) | 4 |
| [XSS](./checklists/xss/) | 3 |
| [API Security](./checklists/api-security/) | 2 |
| [Business Logic](./checklists/business-logic/) | 2 |
| [Information Disclosure](./checklists/information-disclosure/) | 2 |
| [OAuth / SSO](./checklists/oauth-sso/) | 2 |
| [Race Condition](./checklists/race-condition/) | 2 |
| [Cache Poisoning](./checklists/cache-poisoning/) | 1 |
| [CORS](./checklists/cors/) | 1 |
| [Path Traversal](./checklists/path-traversal/) | 1 |
| [Privilege Escalation](./checklists/privilege-escalation/) | 1 |
| [Prompt Injection / AI](./checklists/prompt-injection/) | 1 |
| [SSRF](./checklists/ssrf/) | 1 |
| [Subdomain Takeover](./checklists/subdomain-takeover/) | 1 |
| [XXE / XML](./checklists/xxe/) | 1 |

Full folder list: [`checklists/`](./checklists/)

---

## How the data is organized

Simple layout so the repo stays readable as it grows:

```text
checklists/
  broken-access-control/
    <id>.md          ← one checklist card
  authentication/
    <id>.md
  ...

index/
  catalog.json       ← all card summaries (for the live UI)
  categories/        ← per-category summaries
  manifest.json      ← totals + category list
```

- **Source of truth:** Markdown files under `checklists/`
- **Each file:** frontmatter (title, author, tags, quick test) + steps + commands
- **Indexes:** lightweight JSON for search/UI - not a dump of full article text

Example card: [`examples/sample-checklist.md`](./examples/sample-checklist.md)

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
