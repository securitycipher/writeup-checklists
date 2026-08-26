---
id: fdb4d1cedd96
title: "Indirect Prompt Injection: What LLM Bounty Triagers Actually Reward"
source_url: https://medium.com/infosec-writes-up/indirect-prompt-injection-what-llm-bounty-triagers-actually-reward-50bb08fc7dd3
author: "Muhammad Haider Tallal"
publication_date: 2026-08-09
category: prompt-injection
category_label: "Prompt Injection / AI Agent"
content_type: vuln_writeup
steps_source: ai_inferred
tags:
  - "prompt-injection-attack"
  - "ai-security"
  - "bug-bounty"
  - "cybersecurity"
  - "artificial-intelligence"
tools:
  []
quick_test: "Test AI applications by embedding hidden instructions in task submissions to evaluate if they can manipulate the AI's behavior."
---

## Use case

The article discusses how indirect prompt injection can lead to significant security impacts in AI applications, particularly when malicious tasks are embedded in workflows, such as Jira tickets, which can manipulate the AI's memory and behavior.

## Steps to test

1. Identify an AI application that utilizes prompt inputs, such as a chatbot or LLM.
2. Create a Jira ticket or similar task that includes a hidden instruction or malicious prompt.
3. Submit the task and monitor the AI's response to determine if it executes the hidden instruction.
4. Evaluate the impact of the AI's behavior change, particularly if it leads to data loss or manipulation.

## Commands

```text
POST https://example.com/api/task
Content-Type: application/json
Body: {"task": "Create a new entry with hidden instruction: [malicious prompt]"}
```

## Source

- Author: Muhammad Haider Tallal
- Writeup: https://medium.com/infosec-writes-up/indirect-prompt-injection-what-llm-bounty-triagers-actually-reward-50bb08fc7dd3

_For authorized testing only. Credit the original author._
