---
id: ebedc43cd2aa
title: "IntroToBurp - picoCTF Writeup"
source_url: https://medium.com/@may.hack/introtoburp-picoctf-writeup-573152971547
author: "mayhack"
publication_date: 2026-08-24
category: authentication
category_label: "Authentication / Password Reset"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "cybersecurity"
  - "hacking"
  - "bug-bounty"
  - "ctf"
tools:
  - "Burp Suite"
quick_test: "Test for improper server-side validation by intercepting requests and modifying required parameters like OTP to check for authentication bypass."
---

## Use case

The challenge involved a 2FA OTP verification page that could be bypassed by modifying the OTP parameter in the HTTP request. This vulnerability is critical as it allows unauthorized access to sensitive information without proper authentication.

## Steps to test

1. Open the challenge website and fill in the registration form with arbitrary details.
2. Submit the registration form to reach the 2FA OTP page.
3. Enter any value into the OTP field and submit it to trigger the OTP verification.
4. Open Burp Suite and configure your browser to use Burp's proxy.
5. Enable Proxy → Intercept → Intercept is ON.
6. Submit another OTP from the browser to intercept the request.
7. Locate the 'otp' parameter in the intercepted request.
8. Remove the value after 'otp=' and forward the modified request.

## Commands

```text
Register with arbitrary details
Proxy → Intercept → Intercept is ON
otp=123456
otp=
Register
picoCTF{#0TP_Bypvss_SuCc3$S_6bffad21}
```

## Source

- Author: mayhack
- Writeup: https://medium.com/@may.hack/introtoburp-picoctf-writeup-573152971547

_For authorized testing only. Credit the original author._
