id: 043i7ua2e
kind: issue
title: ledger recovery loops forever on a renamed baseline: jj diff --summary shows {old => new}, which qew treats as a path
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-28T17:12:05Z
evidence: 4492e920 52bce2c5
---
## Goal

dirty_owned, the stray sweep and changed_between expand a rename into its real old and new paths, so recovery commits the rename once and converges
