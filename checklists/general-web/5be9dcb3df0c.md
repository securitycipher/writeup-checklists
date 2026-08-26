---
id: 5be9dcb3df0c
title: "Glitch Cat - picoCTF Writeup"
source_url: https://medium.com/@may.hack/glitch-cat-picoctf-writeup-91769f285b24
author: "mayhack"
publication_date: 2026-08-18
category: general-web
category_label: "General Web Security"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "bug-bounty"
  - "ctf"
  - "hacking"
  - "cybersecurity"
tools:
  []
quick_test: "Connect to a service that outputs encoded data and decode any hexadecimal values to retrieve hidden information."
---

## Use case

The challenge involved a flag printing service that partially obfuscated the flag using Python's chr() function with hexadecimal values. This matters because it demonstrates how simple encoding can be exploited to reveal sensitive information.

## Steps to test

1. Use nc to connect to the challenge service: nc saturn.picoctf.net 53501.
2. Observe the output from the service, which includes visible and encoded parts of the flag.
3. Identify the chr(0x..) values in the output.
4. Convert each hexadecimal value to its corresponding ASCII character.
5. Reconstruct the complete flag by combining the visible part with the decoded characters.

## Commands

```text
nc saturn.picoctf.net 53501
chr(0x61)
chr(0x34)
chr(0x33)
chr(0x39)
chr(0x32)
chr(0x64)
chr(0x65)
0x61 → a
0x34 → 4
0x33 → 3
'picoCTF{gl17ch_m3_n07_' + chr(0x61) + chr(0x34) + chr(0x33) + chr(0x39) + chr(0x32) + chr(0x64) + chr(0x32) + chr(0x65) + '}'
```

## Source

- Author: mayhack
- Writeup: https://medium.com/@may.hack/glitch-cat-picoctf-writeup-91769f285b24

_For authorized testing only. Credit the original author._
