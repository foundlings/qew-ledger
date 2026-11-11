id: 044banqdi
kind: issue
title: pr ready takes several numbers: one snapshot, concurrent forge flips
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-11T15:37:50Z
---
## Problem

qew pr ready accepts one number, so marking a union of 12 draft PRs ready is 12 serial processes, each with its own snapshot and forge call. pr merge N1..N8 already batches (6.53.1). Wanted: qew pr ready N1 N2 ... with one shared snapshot, concurrent forge draft-to-ready calls, per-number results, same refusals and exit codes as the single form.

## Done when

pr ready 1 2 3 takes one snapshot and flips concurrently; refusal order and exit codes match the single form
