---
id: 6de0b2a5a7ab
title: "Single Sign On (SSO) Login vulnerabilities"
source_url: https://medium.com/@koushaniot7/single-sign-on-sso-login-vulnerabilities-f4d35c5b7073
author: "wann4beSh3rl0ck"
publication_date: 2026-08-21
category: oauth-sso
category_label: "OAuth / SSO"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "bug-bounty"
  - "auth"
tools:
  - "curl"
quick_test: "Check for hidden iframes in SSO implementations that use postMessage without origin validation."
---

## Use case

The vulnerability exists in the SSO login flow where a hidden iframe is used to silently authenticate users. This can lead to unauthorized access if an attacker can exploit the postMessage mechanism to retrieve sensitive tokens.

## Steps to test

1. Identify an application that uses SSO with a hidden iframe for authentication.
2. Monitor network requests to find the IdP's auth endpoint being called with 'prompt=none'.
3. Observe the iframe's callback URL for the presence of a token or authorization code.
4. Check if the postMessage is implemented as 'parent.postMessage({type: 'onload', data: window.location.href}, '*')'.
5. Test if the application accepts messages from the iframe without validating the origin.
6. Attempt to load the iframe in a controlled environment and capture the token/code being sent to the parent.

## Commands

```text
curl -X GET 'https://example.com/sso/auth?prompt=none'
curl -X POST 'https://example.com/sso/callback' -H 'Content-Type: application/json' -d '{"type": "onload", "data": "https://example.com/callback?token=YOUR_TOKEN"}'
```

## Source

- Author: wann4beSh3rl0ck
- Writeup: https://medium.com/@koushaniot7/single-sign-on-sso-login-vulnerabilities-f4d35c5b7073

_For authorized testing only. Credit the original author._
