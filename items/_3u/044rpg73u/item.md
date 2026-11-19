id: 044rpg73u
kind: issue
title: A dead jj packed-refs.lock is named stale at once (jj's own error wording matched no lock pattern, so writes waited out the whole lock wait)
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-11-19T06:58:37Z
evidence: nursmtwprqru
---
## Problem

Santa 2026-11-19: a zero-byte .git/packed-refs.lock left by a killed process made every write wait 300s and roll back with a generic held message; jj prints 'Could not lock packed refs ... The lockfile at ... might need manual deletion', which qew's LOCK_ERROR never matched.

## Done when

A write meeting a dead (60s+, open in no process) lock fails at once naming the file and qew unlock --stale; a young lock is waited for then named held; qew never removes a lock itself.
