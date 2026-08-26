---
id: 8960cdecdbad
title: "I Analyzed 81 Race Condition Reports on HackerOne - 5 Patterns Kept Appearing"
source_url: https://medium.com/@rajnamdev/i-analyzed-81-race-condition-reports-on-hackerone-5-patterns-kept-appearing-57e0b2ac9916
author: "Raj Namdev"
publication_date: 2026-08-18
category: race-condition
category_label: "Race Condition"
content_type: vuln_writeup
steps_source: ai_inferred
tags:
  - "bug-bounty"
  - "ethical-hacking"
  - "cybersecurity"
  - "web-security"
  - "race-condition"
tools:
  - "curl"
quick_test: "Test for race conditions by sending concurrent requests to sensitive endpoints to see if actions can be performed multiple times."
---

## Use case

Race conditions can lead to financial exploitation, such as redeeming a gift card multiple times or bypassing security measures like 2FA, allowing attackers to gain unauthorized access to accounts.

## Steps to test

1. Identify a feature that allows concurrent requests, such as a gift card redemption or account change.
2. Send multiple concurrent requests to the endpoint using a tool like Turbo Intruder.
3. Monitor the responses to determine if the action was performed multiple times instead of once.
4. For account takeover, attempt to change an email or reset 2FA while sending parallel requests.

## Commands

```text
curl -X POST https://example.com/redeem -d 'gift_card_code=YOUR_GIFT_CARD_CODE' -H 'Content-Type: application/json'
curl -X POST https://example.com/change-email -d 'new_email=attacker@example.com' -H 'Content-Type: application/json'
```

## Source

- Author: Raj Namdev
- Writeup: https://medium.com/@rajnamdev/i-analyzed-81-race-condition-reports-on-hackerone-5-patterns-kept-appearing-57e0b2ac9916

_For authorized testing only. Credit the original author._
