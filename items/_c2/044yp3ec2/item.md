id: 044yp3ec2
kind: issue
title: A renamed ledger file is committed as two paths
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T18:13:14Z
evidence: xoloszow txpxzyvk ltzroqtn
---
## Problem

git status porcelain printed a rename as old -> new and that line went to git add as one path, so qew pr ready 8283 on foundlings left its forge change out of the ledger.

## Done when

a staged or unstaged rename commits
