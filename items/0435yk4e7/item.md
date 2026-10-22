id: 0435yk4e7
kind: issue
title: Inconsistent claim view: start says claimed by 887, take-over and complete say unclaimed (04354zbgp)
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-22T15:07:59Z
discovered_from: 0435ydxgy
---
## Problem

On foundlings item 04354zbgp, qew start said claimed by 887 on the primary while qew start --take-over and qew complete said unclaimed; only qew release --force cleared it. Foundlings item 0435yj9fs logs the symptom.

## Fix

Find which two views of the claim disagree (primary forge assignee vs ledger fold), make every command read one claim view, and heal or report the disagreement.
