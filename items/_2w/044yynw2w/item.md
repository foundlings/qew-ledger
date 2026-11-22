id: 044yynw2w
kind: issue
title: Read a pull request through one GraphQL query
parent: 044yyj516
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T21:28:21Z
evidence: ymvzwzxk sssqknwl vssnzzun ymxkxlvw
---
## Problem

read_pull_request is 3 REST calls plus the verbs' repeats.

## Done when

read_pull_request, find_open_pull_requests and the write verbs' reads use one GraphQL query with checks, REST is the fallback, a parity walk compares both
