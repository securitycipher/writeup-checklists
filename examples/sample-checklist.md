---
id: 9d4d4e15e022
title: "I Changed One User_Id and the API Said Sure - From Password Reset to Mass Account Takeover"
source_url: https://infosecwriteups.com/i-changed-one-user-id-and-the-api-said-sure-from-password-reset-to-mass-account-takeover-9d4d4e15e022
author: Rajdip Chavan
publication_date: 2026-08-24
category: broken-access-control
content_type: vuln_writeup
steps_source: extracted
tags:
  - idor
  - password-reset
  - ato
  - bug-bounty
tools:
  - Burp Repeater
quick_test: "Test password-reset endpoints for IDOR by swapping User_Id to another account without re-auth."
---

## Use case

Password reset (or a similar account workflow) trusted a client-supplied user identifier. Changing that id let the hunter act on other accounts - classic broken access control with ATO impact.

## Steps to test

1. Create two accounts (attacker + victim) on an in-scope target.
2. Start a password-reset (or similar) flow for the attacker account and capture the request in Burp.
3. Locate the user identifier field (`user_id`, `uid`, `accountId`, etc.).
4. Replace it with the victim's identifier and replay.
5. Confirm whether the response or follow-up email/token applies to the victim.
6. Document impact (reset link, session, PII) before reporting.

## Commands

```http
POST /api/password-reset HTTP/1.1
Host: target.example
Content-Type: application/json

{"user_id":"VICTIM_ID","email":"attacker@example.com"}
```

## Notes

Example card for format only. Always test within authorized scope. Link and credit the original writeup author.
