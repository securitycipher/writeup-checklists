---
id: e0ef57efd62f
title: "Restoring Permanently Deleted Projects via IDOR"
source_url: https://medium.com/@abdulrahmanreda660/restoring-permanently-deleted-projects-via-idor-7c8d8c2e3e94
author: "Abdulrahman Reda"
publication_date: 2026-08-16
category: idor
category_label: "IDOR"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "cybersecurity"
  - "bug-bounty"
  - "privilege-escalation"
  - "broken-access-control"
  - "idor"
tools:
  - "Burp Suite"
quick_test: "Check if deleted resources can be accessed or restored by manipulating object references in the URL."
---

## Use case

The application allowed access to permanently deleted projects via insecure direct object reference, enabling unauthorized users to restore these projects, which could lead to data exposure or manipulation.

## Steps to test

1. Log in as a Manager and create a project named 'TEST'.
2. Log in as an Owner and delete the 'TEST' project.
3. Refresh the Manager session and confirm the project is no longer visible.
4. Copy the URL of the deleted project from the Manager session.
5. Change the project ID in the URL to a known deleted project ID.
6. Access the modified URL as the Owner and restore the deleted project.

## Commands

```text
GET https://example.com/projects/{existing-project-id}
GET https://example.com/projects/{deleted-project-id}
https://example.com/projects/{existing-project-id}
https://example.com/projects/{deleted-project-id}
```

## Source

- Author: Abdulrahman Reda
- Writeup: https://medium.com/@abdulrahmanreda660/restoring-permanently-deleted-projects-via-idor-7c8d8c2e3e94

_For authorized testing only. Credit the original author._
