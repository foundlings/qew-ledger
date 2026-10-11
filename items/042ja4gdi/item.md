id: 042ja4gdi
kind: task
title: Drop a checklist item from a pull request
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-11T21:03:01Z
---
## Problem

A checklist item the PR will not finish blocks the merge and cannot be removed or unticked; the workaround is close and reopen

## Done when

qew pr check N --drop ID --reason TEXT removes that box, keeps every other tick, records drop and reason on item and PR record, refuses a ticked box without --force
