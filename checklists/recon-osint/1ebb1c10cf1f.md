---
id: 1ebb1c10cf1f
title: "NetBIOS & SMB Enumeration :"
source_url: https://medium.com/@divyanshukr4246/netbios-smb-enumeration-50f2cc82f6b2
author: "Divyanshu Chaudhary"
publication_date: 2026-08-23
category: recon-osint
category_label: "Recon / OSINT"
content_type: practical_guide
steps_source: extracted
tags:
  - "bug-bounty"
  - "enumeration"
  - "cybersecurity"
  - "reconnaissance"
tools:
  - "nmap"
quick_test: "Run nmap and nbtscan against the target to identify open NetBIOS and SMB services."
---

## Use case

NetBIOS and SMB enumeration can reveal sensitive information about network shares and services running on a target system. This information can be exploited for unauthorized access or further attacks.

## Steps to test

1. Identify the target IP address or hostname.
2. Use nmap to scan for open NetBIOS and SMB ports: 'nmap -p 137,138,139,445 <target_ip>'
3. Perform NetBIOS name service enumeration: 'nbtscan <target_ip>'
4. Use smbclient to list shares on the target: 'smbclient -L //<target_ip> -U guest'
5. Check for SMB version and settings: 'smbclient -m SMB2 -L //<target_ip> -U guest'

## Commands

```text
nmap -p 137,138,139,445 <target_ip>
nbtscan <target_ip>
smbclient -L //<target_ip> -U guest
smbclient -m SMB2 -L //<target_ip> -U guest
Reconnaissance
│
├── Passive Recon
│   └── Collecting publicly available information
│
└── Active Recon / Enumeration
└── Collecting detailed information from specific services
Port            Protocol                    Purpose
------------------------------------------------------
137               UDP                        NetBIOS Name Service (NBNS)
138               UDP                        NetBIOS Datagram Service
139               TCP                        NetBIOS Session Service
Port                 Protocol                Purpose
---------------------------------------------------------
139                  TCP                     SMB over NetBIOS Session Service
445                  TCP                     Direct-hosted SMB over TCP
Modern SMB
│
▼
TCP/445
│
▼
SMB
│
▼
File & Resource Sharing
```

## Source

- Author: Divyanshu Chaudhary
- Writeup: https://medium.com/@divyanshukr4246/netbios-smb-enumeration-50f2cc82f6b2

_For authorized testing only. Credit the original author._
