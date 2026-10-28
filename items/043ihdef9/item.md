id: 043ihdef9
kind: issue
title: qew pr open, ready, close and merge hold the ledger write lock across forge HTTP; do the forge calls outside it
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-28T20:26:59Z
---
## Goal

the ledger write lock covers only the ledger reads and writes of pr verbs; forge requests run before or after it, so a slow forge cannot hold every writer
