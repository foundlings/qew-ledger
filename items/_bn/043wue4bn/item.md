id: 043wue4bn
kind: issue
title: Support optional named remotes for code and ledger operations
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-04T11:21:59Z
---
## Problem

Hardcoded origin prevents using an alternate remote during a protocol outage even when origin2 reaches the same repository.

## Fix

Add optional --remote and --ledger-remote selectors, retain origin defaults, consistently select fetch push merge tracking and evidence refs for git and jj, document and release.

## Done when

Offline command walks prove alternate remotes work with unreachable origin, invalid names are refused, defaults remain compatible, full gate passes and a new release is published.
