id: 044qfc16d
kind: issue
title: qew check --stale-claims: claimed items with no open PR and no recent activity
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-18T15:57:51Z
discovered_from: 044qdr89f
evidence: ntswkzot
---
## Problem

The claim identity is shared (887), so claimed says nothing about a live worker; 151 claimed items had no open PR and no commit ref in 24h.

## Done when

qew check --stale-claims [--hours N] lists them with last activity, json too
