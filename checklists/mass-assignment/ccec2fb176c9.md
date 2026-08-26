---
id: ccec2fb176c9
title: "Mass Assignment: How \"isAdmin\":true Still Works in 2026"
source_url: https://kd-200.medium.com/mass-assignment-how-isadmin-true-still-works-in-2026-599a0f6b61ba
author: "Nitin yadav"
publication_date: 2026-08-20
category: mass-assignment
category_label: "Mass Assignment"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "bug-bounty-tips"
  - "infosec"
  - "bug-bounty"
  - "info-sec-writeups"
  - "cybersecurity"
tools:
  []
quick_test: "Check if the application allows mass assignment by modifying user profile fields that are not exposed in the UI."
---

## Use case

The application allows users to update their profile but fails to restrict which fields can be modified, leading to potential privilege escalation by allowing unauthorized changes to sensitive fields like 'isAdmin'.

## Steps to test

1. Log in to the application and navigate to the profile update section.
2. Use a tool like Burp Suite to intercept the request when updating your profile.
3. Capture the normal PATCH request, which includes fields like 'name' and 'email'.
4. Modify the captured request to include 'isAdmin': true in the JSON body.
5. Send the modified request to the server.
6. Verify if your user role has changed to admin.

## Commands

```text
PATCH /api/profile
{"name":"your_name","email":"your_email@example.com","isAdmin":true}
PATCH /api/profile
{"name":"nitin","email":"a@a.com"}
```

## Source

- Author: Nitin yadav
- Writeup: https://kd-200.medium.com/mass-assignment-how-isadmin-true-still-works-in-2026-599a0f6b61ba

_For authorized testing only. Credit the original author._
