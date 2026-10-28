id: 042epuq1n
kind: issue
title: Import and plan validation names every problem, not only the first
parent: 
needs: 
labels: 
owner: 
priority: 3
created: 2026-10-09T14:30:40Z
---
## Problem

qew import DIR and create --from-file stop at the first refusal (one label over 50 characters out of 1614) and write nothing, so a large import needs one retry per problem class.

## Fix

Validation collects problems across the whole plan and prints them grouped with counts (bounded), still exiting 2 with nothing written.

## Done when

A walk with three kinds of bad entries sees all three named in one run.
