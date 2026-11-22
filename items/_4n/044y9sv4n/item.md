id: 044y9sv4n
kind: issue
title: A background sync must never drain the shared token: reset-aware waits and a call reserve
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-11-22T13:21:15Z
---
## Where

src/qew/forge_http.py, forge_retry.py

## Problem

Foundlings' shared GitHub token hit remaining 0 (403, reset 13:41Z) and every merge failed. Background pulls (50+ pages each before 7.1.2) and retries spent the budget: nothing stopped the worker at a reserve, and a 403 with x-ratelimit-remaining 0 was retried six times on a 30 s guess instead of honouring x-ratelimit-reset.

## Fix

Background worker stands down below a 500-call reserve; an exhausted limit that lifts within the cap waits until the reset, one further away is reported once with the retry time; interactive verbs are not held back.

## Done when

Walks show the worker makes no calls below the reserve, an exhausted limit with a far reset is not retried, and one with a near reset waits until it.
