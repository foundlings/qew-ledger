id: 043ih2sfp
kind: issue
title: sync worker takes lock first, then push.lock, so it never sits on push.lock while queued behind writers
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-28T20:20:47Z
---
## Goal

the sync finishing step and checkpoint acquire the write lock before the push lock, so push.lock is held only while committing and pushing
