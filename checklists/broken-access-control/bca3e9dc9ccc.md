---
id: bca3e9dc9ccc
title: "I Ranked 252 Disclosed IDOR Reports by Bounty. Severity Barely Mattered."
source_url: https://medium.com/@rajnamdev/i-ranked-252-disclosed-idor-reports-by-bounty-severity-barely-mattered-3ba306bfa595
author: "Raj Namdev"
publication_date: 2026-08-23
category: broken-access-control
category_label: "Broken Access Control / IDOR"
content_type: vuln_writeup
steps_source: ai_inferred
tags:
  - "cybersecurity"
  - "web-security"
  - "bug-bounty"
  - "ethical-hacking"
  - "idor"
tools:
  []
quick_test: "Test for IDOR by swapping user identifiers in API requests to access unauthorized data."
---

## Use case

The vulnerability allows unauthorized access to sensitive billing documents of other users through a GraphQL API by manipulating user identifiers. This is critical as it exposes personal and financial information.

## Steps to test

1. Identify the GraphQL API endpoint responsible for fetching billing documents.
2. Capture a valid request that retrieves your own billing document.
3. Modify the user identifier in the request payload to that of another user.
4. Send the modified request and observe the response for unauthorized access to another user's billing information.

## Commands

```text
POST https://example.com/graphql
Content-Type: application/json
Body: { 'query': 'query { billingDocument(userId: "TARGET_USER_ID") { email, address, invoiceContents, cardLastFour, cardType } }' }
```

## Source

- Author: Raj Namdev
- Writeup: https://medium.com/@rajnamdev/i-ranked-252-disclosed-idor-reports-by-bounty-severity-barely-mattered-3ba306bfa595

_For authorized testing only. Credit the original author._
