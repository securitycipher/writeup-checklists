---
id: 076ee0f4bedc
title: "LandRocker Bug Bounty Program"
source_url: https://landrocker.medium.com/landrocker-bug-bounty-program-aa2f55f47297
author: "LandRocker"
publication_date: 2023-11-15
category: general-web
category_label: "General Web Security"
content_type: vuln_writeup
steps_source: ai_inferred
tags:
  - "bug-bounty"
  - "bitcoin"
  - "cryptocurrency-investment"
  - "token-sale"
  - "web3"
tools:
  []
quick_test: "Test the token purchase and bug reporting features for input validation vulnerabilities by submitting unexpected payloads."
---

## Use case

The LandRocker Bug Bounty Program allows beta players to purchase tokens and report bugs during the buying process. A vulnerability in this flow could lead to unauthorized access to token purchases or exploitation of the bug reporting feature.

## Steps to test

1. Navigate to the LandRocker token sale page.
2. Attempt to purchase tokens using various payment methods to identify any potential flaws in the transaction process.
3. Use the 'report bug' button to submit a bug report with different payloads to test for input validation issues.
4. Monitor the response for any error messages or unexpected behavior that could indicate a vulnerability.

## Commands

```text
POST https://example.com/token-sale/buy HTTP/1.1
Content-Type: application/json
Body: { 'amount': '100', 'payment_method': 'credit_card' }
GET https://example.com/token-sale/report-bug HTTP/1.1
Body: { 'description': '<script>alert(1)</script>' }
```

## Source

- Author: LandRocker
- Writeup: https://landrocker.medium.com/landrocker-bug-bounty-program-aa2f55f47297

_For authorized testing only. Credit the original author._
