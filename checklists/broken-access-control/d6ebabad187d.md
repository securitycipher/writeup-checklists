---
id: d6ebabad187d
title: "Google Classroom IDOR Vulnerability POC Video"
source_url: https://marrijalikhan.medium.com/google-classroom-idor-vulnerability-poc-video-c0201d18dd04
author: "Marrij Ali Khan"
publication_date: 2026-08-22
category: broken-access-control
category_label: "Broken Access Control / IDOR"
content_type: vuln_writeup
steps_source: ai_inferred
tags:
  - "info-sec-writeups"
  - "idor-vulnerability"
  - "bug-bounty-writeup"
  - "bug-bounty"
  - "google"
tools:
  []
quick_test: "Test for IDOR by manipulating object IDs in requests to see if unauthorized data can be accessed."
---

## Use case

The vulnerability in Google Classroom allowed unauthorized access to objects that should have been restricted, demonstrating a critical flaw in access control mechanisms.

## Steps to test

1. Log in to Google Classroom with valid credentials.
2. Capture the request made to access a specific resource (e.g., a class or assignment).
3. Modify the request to change the object ID parameter to that of another user's resource.
4. Send the modified request and observe if unauthorized access is granted.

## Commands

```text
GET https://classroom.googleapis.com/v1/courses/{courseId}/students
GET https://classroom.googleapis.com/v1/courses/{anotherCourseId}/students
```

## Source

- Author: Marrij Ali Khan
- Writeup: https://marrijalikhan.medium.com/google-classroom-idor-vulnerability-poc-video-c0201d18dd04

_For authorized testing only. Credit the original author._
