---
id: dfa30a38a2db
title: "How a 30-Year-Old Path Traversal Earned $150K From Apple's AI Cloud"
source_url: https://infosecwriteups.com/how-a-30-year-old-path-traversal-earned-150k-from-apples-ai-cloud-f7d6b8df1f25
author: "Abhishek meena"
publication_date: 2026-08-12
category: path-traversal
category_label: "Path Traversal / Arbitrary File Read"
content_type: vuln_writeup
steps_source: ai_inferred
tags:
  - "bug-bounty-tips"
  - "infosec"
  - "bug-bounty"
  - "apple"
  - "bug-bounty-writeup"
tools:
  - "curl"
quick_test: "Test for path traversal vulnerabilities by crafting tar files with malicious paths and observing if the system allows writing to unauthorized locations."
---

## Use case

The vulnerability was found in the darwin-init process of Apple's Private Cloud Compute, which allowed an attacker to exploit a path traversal flaw to write files as root, thereby compromising the system's integrity and redirecting AI telemetry.

## Steps to test

1. Identify the darwin-init process running as PID 1 on the target system.
2. Create a crafted tar file that contains a malicious file path.
3. Use the archive extractor in darwin-init to extract the tar file.
4. Verify that the crafted file has been written to a persistent location with root privileges.

## Commands

```text
curl -X POST -H 'Content-Type: application/x-tar' --data-binary @malicious.tar http://example.com/extract
```

## Source

- Author: Abhishek meena
- Writeup: https://infosecwriteups.com/how-a-30-year-old-path-traversal-earned-150k-from-apples-ai-cloud-f7d6b8df1f25

_For authorized testing only. Credit the original author._
