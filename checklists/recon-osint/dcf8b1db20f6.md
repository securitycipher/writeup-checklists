---
id: dcf8b1db20f6
title: "100 High-Value Files & Paths Every Bug Hunter Should Check During Recon"
source_url: https://medium.com/@getroutenet196/100-high-value-files-paths-every-bug-hunter-should-check-during-recon-8b6900b20ff4
author: "Tejas Kamble"
publication_date: 2026-08-04
category: recon-osint
category_label: "Recon / OSINT"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "pentesting"
  - "reconnaissance"
  - "bug-bounty"
  - "web-security"
  - "cybersecurity"
tools:
  []
quick_test: "Run a check for common sensitive files and paths on the target domain to identify potential information leaks."
---

## Use case

During reconnaissance, a bug hunter can identify sensitive files and paths that may expose critical information such as credentials or source code. This is crucial as it helps in understanding the application's attack surface before attempting to exploit vulnerabilities.

## Steps to test

1. Confirm the target domain is in scope.
2. Identify the application technology stack using tools like Wappalyzer.
3. Check for the presence of high-value files such as /.env, /config.php, and /wp-config.php.
4. Assess the accessibility of these files and determine if they expose sensitive information.
5. Evaluate the impact of the exposed information to prioritize further testing.

## Commands

```text
GET https://example.com/.env
GET https://example.com/config.php.bak
GET https://example.com/wp-config.php
GET https://example.com/database.sql
GET https://example.com/backup.zip
/robots.txt
/config.php.bak
DB_HOST=
DB_USERNAME=
DB_PASSWORD=
API_KEY=
SECRET_KEY=
APP_SECRET=
Vulnerability
Critical vulnerability
```

## Source

- Author: Tejas Kamble
- Writeup: https://medium.com/@getroutenet196/100-high-value-files-paths-every-bug-hunter-should-check-during-recon-8b6900b20ff4

_For authorized testing only. Credit the original author._
