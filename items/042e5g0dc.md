id: 042e5g0dc
kind: issue
title: A plain sync recovers when the forge repo was recreated
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-09T07:54:45Z
---
## Problem

After the forge repo is deleted and recreated, every mirrored issue 404s: sync reports one failure per item and records a divergence per item; only a hand-run qew restore recovers.

## Fix

When a full pull finds a complete listing with none of the mirrored issues present, sync forgets those mirrors and recreates them (the restore path), reporting one line, without recording divergences.

## Done when

A walk deletes every issue on the fake forge, runs plain qew sync, and sees all issues recreated, mirrors renumbered, no conflicts.
