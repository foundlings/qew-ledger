id: 043ix2f9t
kind: issue
title: GitHub caps a parent at 100 sub-issues: sync records the 422 as a known condition instead of failing every sync
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-29T01:26:50Z
evidence: b1c7edfd 6935e1ac
---
## Goal

a sub-issue add refused with 'cannot have more than 100 sub-issues' is recorded once on the mirror as not mirrored (parent at the cap), is not retried, and does not make sync finish with failures
