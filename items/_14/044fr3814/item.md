id: 044fr3814
kind: issue
title: pr merge waits for the forge to compute mergeable instead of refusing at once
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-13T20:31:28Z
evidence: okpvlzxr vvvrktwz
---
## Problem

GitHub returns mergeable null for seconds after a push or base move; pr merge and --check refuse 'merge state unknown, retry in a moment' and the foundlings merge gate fails as gate_refused. Requested by Santa.

## Done when

A merge-state read that is None is re-read with backoff 1,2,4,8,15,30 s (60 s) in pr merge, --check and the batch read, then gated normally; only after the budget does it refuse, saying how long it waited. Sleep is injectable.
