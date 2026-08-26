---
id: d77d9e7bdee6
title: "How I Got My NASA Hall of Fame: A Unique Twist on Google Dorking"
source_url: https://vanshrathorebughunter.medium.com/how-i-got-my-nasa-hall-of-fame-a-unique-twist-on-google-dorking-a954193b317f
author: "Vanshrathore"
publication_date: 2026-08-05
category: information-disclosure
category_label: "Information Disclosure"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "bug-bounty"
  - "penetration-testing"
  - "bug-bounty-writeup"
  - "money"
  - "bug-bounty-tips"
tools:
  []
quick_test: "Search for old articles on trusted domains using Google Dorks and check for broken links that could lead to brand impersonation."
---

## Use case

A broken link on a trusted NASA domain could lead to brand impersonation, allowing attackers to create phishing pages that appear legitimate to users clicking the link.

## Steps to test

1. Use Google Dorks to search for old articles on the NASA domain.
2. Look for social media links within the articles.
3. Identify any typographical errors in the URLs of those links.
4. Register the misspelled URL to demonstrate the potential for brand impersonation.

## Commands

```text
site:nasa.gov ("facebook.com" OR "instagram.com" OR "twitter.com" OR "youtube.com")
site:*.nasa.gov ("facebook.com" OR "instagram.com" OR "twitter.com" OR "youtube.com")
site:*.*.nasa.gov ("facebook.com" OR "instagram.com" OR "twitter.com" OR "youtube.com")
site:example.com ("facebook.com" OR "instagram.com" OR "twitter.com" OR "youtube.com")
site:*.example.com ("facebook.com" OR "instagram.com" OR "twitter.com" OR "youtube.com")
site:*.*.example.com ("facebook.com" OR "instagram.com" OR "twitter.com" OR "youtube.com")
```

## Source

- Author: Vanshrathore
- Writeup: https://vanshrathorebughunter.medium.com/how-i-got-my-nasa-hall-of-fame-a-unique-twist-on-google-dorking-a954193b317f

_For authorized testing only. Credit the original author._
