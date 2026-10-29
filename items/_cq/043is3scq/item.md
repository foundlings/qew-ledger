id: 043is3scq
kind: issue
title: a background sync that exits on a held sync.lock can strand the id its write queued: the running worker must look at the queue again after it releases the lock
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-28T23:45:32Z
evidence: 4393d65a 9fbde368
---
## Goal

after a worker releases sync.lock it starts another when sync.queue is not empty, so a burst of writes always ends with every item synced
