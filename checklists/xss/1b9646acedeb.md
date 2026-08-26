---
id: 1b9646acedeb
title: "Web Encoding for Beginners: URL, HTML, Unicode, Base64 & Hex"
source_url: https://medium.com/@ph620095/web-encoding-for-beginners-url-html-unicode-base64-hex-e944bff8fcf5
author: "Ph"
publication_date: 2026-08-15
category: xss
category_label: "XSS"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "hacking"
  - "web-development"
  - "bug-bounty"
  - "hacker"
  - "cybersecurity"
tools:
  []
quick_test: "Always ensure user input is contextually encoded based on where it will be displayed (HTML, attribute, JS, URL, CSS) to prevent XSS vulnerabilities."
---

## Use case

Web applications that reflect user input without proper encoding may be vulnerable to XSS attacks. This occurs when special characters are not encoded correctly, allowing attackers to inject malicious scripts.

## Steps to test

1. Identify a web application that reflects user input in HTML output.
2. Submit a payload containing special characters, such as <script>alert('XSS')</script>, in a form field or URL parameter.
3. Observe the response to check if the payload is executed in the browser.
4. If the payload is executed, the application is vulnerable to XSS due to improper encoding.

## Commands

```text
GET https://example.com/search?note=<script>alert('XSS')</script>
```

## Source

- Author: Ph
- Writeup: https://medium.com/@ph620095/web-encoding-for-beginners-url-html-unicode-base64-hex-e944bff8fcf5

_For authorized testing only. Credit the original author._
