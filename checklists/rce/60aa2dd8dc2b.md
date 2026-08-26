---
id: 60aa2dd8dc2b
title: "Lab: Using PHAR deserialization to deploy a custom gadget chain"
source_url: https://medium.com/@amrsmooke321/lab-using-phar-deserialization-to-deploy-a-custom-gadget-chain-62715de7bd27
author: "Amrsmooke"
publication_date: 2026-08-10
category: rce
category_label: "RCE / Code Execution"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "portswigger"
  - "bug-bounty"
  - "hacking"
  - "penetration-testing"
  - "burpsuite"
tools:
  []
quick_test: "Test any file upload feature for PHAR deserialization vulnerabilities by uploading a controlled file and attempting to access it using the PHAR wrapper."
---

## Use case

The application allows file uploads and processes them without proper validation, enabling an attacker to exploit PHAR deserialization vulnerabilities to execute arbitrary code. This is critical as it can lead to remote code execution on the server.

## Steps to test

1. Identify a file upload feature on the website, such as an avatar upload or file import tool.
2. Upload a dummy text file named 'test.txt' containing the word 'hello'.
3. Determine the upload path by inspecting the website source or image URL.
4. Use the PHAR wrapper to access the uploaded file by navigating to 'phar://localhost/uploads/test.txt'.
5. Check for errors indicating that the server is attempting to parse the file as a PHAR archive.

## Commands

```text
file_exists($something)
file_get_contents($something)
fopen($something, 'r')
include($something)
phar://localhost/uploads/test.txt
$this->template_file_path
return $this->twig->render('index', ['user' => $this->user]);
file_exists($something)
file_get_contents($something)
fopen($something, 'r')
include($something)
'templates/' . $this->template_file_path . '.lock'
$this->twig->render(...)
```

## Source

- Author: Amrsmooke
- Writeup: https://medium.com/@amrsmooke321/lab-using-phar-deserialization-to-deploy-a-custom-gadget-chain-62715de7bd27

_For authorized testing only. Credit the original author._
