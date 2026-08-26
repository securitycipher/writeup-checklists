---
id: ddf6b41a7cf9
title: "reconFTW: The Automated Recon Framework Every Bug Bounty Hunter Should Know in 2026"
source_url: https://medium.com/@xpert4cyber/reconftw-the-automated-recon-framework-every-bug-bounty-hunter-should-know-in-2026-f7d0d581d896
author: "Xpert4Cyber"
publication_date: 2026-08-16
category: recon-osint
category_label: "Recon / OSINT"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "penetration-testing"
  - "ethical-hacking-training"
  - "cybersecurity"
  - "bug-bounty"
  - "infosec"
tools:
  - "Httpx"
  - "Nuclei"
  - "Subfinder"
quick_test: "Run a deep permutation scan with reconFTW on your target to identify any hidden subdomains that could lead to vulnerabilities."
---

## Use case

The article discusses how deep permutation scanning with reconFTW uncovered a hidden staging subdomain that was missed by manual passive scans, leading to a stored XSS vulnerability. This finding is significant as it highlights the importance of automated tools in identifying overlooked attack surfaces.

## Steps to test

1. Install reconFTW on your system using the provided installation guide.
2. Configure the tool with your target domain.
3. Run the deep permutation scan mode to enumerate subdomains.
4. Review the scan results for any hidden or staging subdomains.
5. Test the identified subdomains for potential vulnerabilities, such as stored XSS.

## Commands

```text
reconftw scan --target example.com --mode deep-permutation
```

## Source

- Author: Xpert4Cyber
- Writeup: https://medium.com/@xpert4cyber/reconftw-the-automated-recon-framework-every-bug-bounty-hunter-should-know-in-2026-f7d0d581d896

_For authorized testing only. Credit the original author._
