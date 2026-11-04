id: 043wwfc18
kind: issue
title: Allow qew land to complete multiple merged pull requests in one call
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-04T12:03:32Z
---
## Problem

Integrators landing a batch of union PRs must invoke qew land once per PR; a multi-number invocation is rejected.

## Fix

Extend qew land NUMBER... with ordered deduplication, per-PR results, independent progress through errors, machine-readable batch output and unchanged single-PR behavior.

## Done when

Command walks cover batch success, duplicates, retries, mixed failures and integrator claims; help README and specs agree; full gate passes and a new release is published.
