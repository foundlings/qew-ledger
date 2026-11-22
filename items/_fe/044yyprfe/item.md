id: 044yyprfe
kind: issue
title: Cache the branch protection lookup per process
parent: 044yyj516
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T21:29:26Z
evidence: ymvzwzxk sssqknwl vssnzzun ymxkxlvw
---
## Problem

requires_status_checks makes 2 REST calls each time a verb asks.

## Done when

asked once per branch per process
