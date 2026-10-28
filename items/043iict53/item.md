id: 043iict53
kind: issue
title: detached sync workers pile up: a losing worker waits for the write lock before it checks sync.lock
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-28T20:47:03Z
---
## Goal

a background sync takes sync.lock first and exits at once when another worker holds it, so one write rate cannot spawn a dozen waiting processes
