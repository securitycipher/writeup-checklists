---
id: ccb776ccba8c
title: "The bug that survived three years of code review"
source_url: https://mayssare.medium.com/the-bug-that-survived-three-years-of-code-review-3645ca2b05f2
author: "Mayssare"
publication_date: 2026-08-22
category: broken-access-control
category_label: "Broken Access Control / IDOR"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "vulnerability-disclosure"
  - "software-engineering"
  - "open-source"
  - "cybersecurity"
  - "bug-bounty"
tools:
  []
quick_test: "Check if the API endpoint validates all parameters against user permissions to prevent unauthorized data access."
---

## Use case

The vulnerability existed in the Frigate NVR system where the job_id parameter was not properly validated against the camera_name, allowing unauthorized access to motion metadata from cameras the user should not have visibility into.

## Steps to test

1. Identify a camera you have access to (e.g., front_yard).
2. Perform a motion search on that camera to obtain a job_id.
3. Modify the request to use a job_id from a different camera (e.g., server_room).
4. Send a GET request to /api/front_yard/search/motion/{that_job_id} with the unauthorized job_id.
5. Observe the response for motion metadata from the unauthorized camera.

## Commands

```text
GET /api/front_yard/search/motion/{that_job_id} HTTP/1.1
Host: example.com
GET /api/{camera_name}/search/motion/{job_id}
GET /api/front_yard/search/motion/{that_job_id}
```

## Source

- Author: Mayssare
- Writeup: https://mayssare.medium.com/the-bug-that-survived-three-years-of-code-review-3645ca2b05f2

_For authorized testing only. Credit the original author._
