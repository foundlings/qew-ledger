id: 043chj98d
kind: issue
title: Batch merge refuses members that conflict with main though the lead head contains them
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-25T21:02:54Z
---
## Where

src/qew/pr_batch.py, src/qew/cmd_pr.py (_merge_gates)

## Problem

qew pr merge A B C preflights every member alone, so a member whose own head conflicts with main is refused although the lead head already contains it and only the lead is merged

## Fix

Skip the conflicts-with-base gate for a member whose head the lead contains; the lead's own gate still applies

## Done when

a batch whose followers conflict with main individually but sit inside a conflict-free lead merges
