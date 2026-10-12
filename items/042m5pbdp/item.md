id: 042m5pbdp
kind: task
title: Release 6.14.1 with automatic ledger push prevention and minimum version 6.14.1
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-12T19:21:41Z
---
Publish the tested empty-checkpoint ledger push fix as 6.14.1. Review specs and README for affected behavior, bump package and repository minimum_version, run the full gate, install the release, push main and tag, publish release notes, and verify qew-ledger is caught up.
