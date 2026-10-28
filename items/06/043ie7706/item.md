id: 043ie7706
kind: issue
title: jj ledger op log grows without bound: sync collects operations older than 14 days automatically
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-28T19:22:07Z
evidence: 83b3a787 304e37cb
---
## Goal

qew sync abandons jj operations older than 14 days (keeping the newest 200) and garbage collects, at most once a day, with no manual step
