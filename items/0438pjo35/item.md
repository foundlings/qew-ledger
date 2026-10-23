id: 0438pjo35
kind: issue
title: qew pr block and unblock: label blocked, title suffix [blocked by: #M], auto-unblock when the blocker merges
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-23T23:47:43Z
---
## Problem

an elf that opens a pull request to clear another pull request's blockage has no way to show it: the blocked pull request carries no label and its title does not say what it waits on.

## Done when

qew pr block N --by M adds the label blocked and the title suffix; qew pr unblock N removes a blocker, the label and suffix when none remain; qew pr sync keeps the suffix; merging or landing M unblocks every pull request blocked by M and prints which; no label ever holds an id
