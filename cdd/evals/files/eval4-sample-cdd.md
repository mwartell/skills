---
date: 2026-04-05
title: auth system refactor
current_head: abc1234
agent: "test"
session_type: refactor
topics: [auth, refactor]
---

# Prompt 1: refactor the login flow

The current login flow has several problems:

1. It mixes business logic with view logic in `login.py`
2. Password validation is duplicated in three places
3. Session tokens are stored insecurely in a plain text file

Please extract the business logic into a new `auth/service.py`, consolidate password validation into `auth/validators.py`, and switch to hashed token storage in a database table.
