---
id: fd0cda5bfb10
title: "How Broken OAuth Flows Turn Into One-Click Account Takeovers"
source_url: https://medium.com/@tanvir.infosec/how-broken-oauth-flows-turn-into-one-click-account-takeovers-a13a67aa36c0
author: "cyber security"
publication_date: 2026-08-23
category: oauth-sso
category_label: "OAuth / SSO"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "cybersecurity"
  - "bug-bounty"
tools:
  []
quick_test: "Verify that the OAuth implementation includes state and PKCE to bind the authorization response to the original login transaction."
---

## Use case

The vulnerable OAuth flow in the PhotoVault application allowed an attacker to exploit the lack of transaction binding, leading to potential account takeover through login CSRF or account linking vulnerabilities. This was critical as it could allow unauthorized access to user accounts without needing the victim's credentials.

## Steps to test

1. Initiate the OAuth login flow by navigating to the login endpoint: /login/exampleid.
2. Capture the authorization code returned in the callback URL after the user authenticates.
3. Manipulate the callback request to include an attacker-controlled authorization code.
4. Send the manipulated callback request to the /oauth/callback endpoint.
5. Observe if the session is created for the attacker instead of the intended user.

## Commands

```text
GET /login/exampleid HTTP/1.1
GET /oauth/callback?code=ATTACKER_AUTHORIZATION_CODE HTTP/1.1
Browser → PhotoVault → ExampleID (auth) → PhotoVault /oauth/callback → session created
@app.get("/oauth/callback")
def callback(code):
tokens = exchange_code(code)
user = get_user_from_tokens(tokens)
session.login(user)
return redirect("/dashboard")
GET /authorize?
client_id=photovault&
redirect_uri=https%3A%2F%2Fphotovault.example%2Foauth%2Fcallback&
response_type=code&
scope=openid%20profile
HTTP/1.1 302 Found
Location: https://photovault.example/oauth/callback?code=AUTHORIZATION_CODE
authorization code → token endpoint → access token / ID token → session
@app.get("/login/exampleid")
def login():
url = (
"https://id.example/authorize"
"?client_id=photovault"
"&response_type=code"
"&redirect_uri=https://photovault.example/oauth/callback"
"&scope=openid%20profile"
)
return redirect(url)
@app.get("/oauth/callback")
def callback(code):
token_response = oauth.exchange_code(code)
identity = token_response["id_token"]
user = find_or_create_user(identity)
session["user_id"] = user.id
return redirect("/dashboard")
Original state:  9f7c...a31
Callback state:  9f7c...a31   → match, accept
```

## Source

- Author: cyber security
- Writeup: https://medium.com/@tanvir.infosec/how-broken-oauth-flows-turn-into-one-click-account-takeovers-a13a67aa36c0

_For authorized testing only. Credit the original author._
