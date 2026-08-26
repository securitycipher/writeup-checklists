---
id: d7cdfdbbed08
title: "The Story of How I Hacked one of the online payment system website"
source_url: https://christmex.medium.com/the-story-of-how-i-hacked-one-of-the-online-payment-system-website-twice-b0ba48ed13db
author: "Jonathan Christian"
publication_date: 2023-11-20
category: injection
category_label: "Injection (SQL / NoSQL)"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "bug-bounty-writeup"
  - "programming"
  - "technology"
  - "cybersecurity"
  - "bug-bounty"
tools:
  []
quick_test: "Test for SQL injection on login pages of subdomains and check for default credentials."
---

## Use case

The vulnerability was found in the admin panel login page of a subdomain, allowing unauthorized access through SQL injection. This was critical as it led to the exposure of sensitive employee files.

## Steps to test

1. Use a subdomain enumeration tool like crt.sh to find subdomains related to the target.
2. Navigate to the admin panel login page, e.g., blog.redacted.com/adminpanel.
3. Attempt SQL injection using the payload: ' or 1=1 limit 1;# -- in the username or password field.
4. If successful, log in with default credentials: username: admin, password: admin.
5. Once logged in, check for file upload functionalities or sensitive data access.

## Commands

```text
' or 1=1 limit 1;# --
username: admin
password: admin
username : admin
password : admin
```

## Source

- Author: Jonathan Christian
- Writeup: https://christmex.medium.com/the-story-of-how-i-hacked-one-of-the-online-payment-system-website-twice-b0ba48ed13db

_For authorized testing only. Credit the original author._
