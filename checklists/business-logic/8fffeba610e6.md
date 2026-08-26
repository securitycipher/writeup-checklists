---
id: 8fffeba610e6
title: "The Bug Worth Lakhs Was Not in the Code. Here It Was and How to Report It Properly."
source_url: https://medium.com/@parag.jadhav21891/the-bug-worth-lakhs-was-not-in-the-code-here-it-was-and-how-to-report-it-properly-22312bca3c5d
author: "Parag Jadhav"
publication_date: 2026-08-13
category: business-logic
category_label: "Business Logic"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "bug-bounty"
  - "generative-ai-tools"
  - "cybersecurity"
  - "business"
  - "ai-security"
tools:
  []
quick_test: "Test if the application allows users to manipulate transaction values or bypass critical steps in a workflow."
---

## Use case

Business logic vulnerabilities arise when a developer's assumptions about user behavior can be exploited, leading to significant security risks such as transaction manipulation or unauthorized access to backend functionality.

## Steps to test

1. Identify a multi-step process in the application that requires user interaction.
2. Attempt to bypass or reorder the steps to see if the application enforces the intended sequence.
3. Manipulate numeric values during a transaction, such as altering amounts or quantities before submission.
4. Provide unexpected input types in fields where the application expects a specific format.
5. Access backend functionality directly via API requests that are not exposed in the user interface.

## Commands

```text
POST /api/transaction HTTP/1.1
Host: example.com
Content-Type: application/json
Body: {"amount": "1000", "quantity": "10", "discount_code": "INVALID_CODE"}
GET /api/backend-functionality HTTP/1.1
```

## Source

- Author: Parag Jadhav
- Writeup: https://medium.com/@parag.jadhav21891/the-bug-worth-lakhs-was-not-in-the-code-here-it-was-and-how-to-report-it-properly-22312bca3c5d

_For authorized testing only. Credit the original author._
