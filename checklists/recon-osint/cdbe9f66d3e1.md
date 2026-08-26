---
id: cdbe9f66d3e1
title: "Dorks that could get you a good bounty in 2026"
source_url: https://medium.com/@thenewdate24/dorks-that-could-get-you-a-good-bounty-in-2026-a8cde06f18ed
author: "Deepanshu Deep"
publication_date: 2026-08-14
category: recon-osint
category_label: "Recon / OSINT"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "cybersecurity"
  - "bug-bounty"
  - "google-dorking"
  - "web-security"
  - "osint"
tools:
  []
quick_test: "Use Google dorking to search for exposed files and directories on a target domain to identify potential security weaknesses."
---

## Use case

The article discusses various Google dorking techniques that can uncover sensitive information, misconfigurations, and exposed files on a target's website. This matters because it helps security researchers identify potential vulnerabilities that could lead to unauthorized access or data breaches.

## Steps to test

1. Identify the target domain you want to assess.
2. Use the command 'intitle:"index of" site:target.com' to find exposed directories.
3. Execute 'site:target.com filetype:log intext:"password"' to search for logs containing sensitive information.
4. Run 'site:target.com inurl:.git' to check for exposed Git repositories.
5. Verify the accessibility of any discovered endpoints or files.

## Commands

```text
intitle:"index of" site:target.com
site:target.com filetype:log site:target.com
site:target.com inurl:phpinfo.php
site:target.com filetype:sql inurl:db
site:target.com inurl:.git
intitle:"index of" site:target.com
filetype:log site:target.com
filetype:sql site:target.com
filetype:env site:target.com
site:target.com inurl:phpinfo.php
site:target.com inurl:admin
site:target.com inurl:backup
site:target.com inurl:wp-
site:target.com filetype:config
site:target.com filetype:ini
site:target.com filetype:json inurl:config
site:target.com filetype:log intext:"password"
site:target.com filetype:log intext:"username"
site:target.com filetype:sql "password"
site:target.com filetype:sql inurl:db
site:target.com filetype:sql inurl:dump
site:target.com filetype:bak inurl:db
```

## Source

- Author: Deepanshu Deep
- Writeup: https://medium.com/@thenewdate24/dorks-that-could-get-you-a-good-bounty-in-2026-a8cde06f18ed

_For authorized testing only. Credit the original author._
