id: 042o3iigx
kind: issue
title: qew doctor and init warn when a jj ledger runs without watchman
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-13T18:26:38Z
---
Watchman cuts a jj snapshot of a 171k-file ledger from 2.0 s to 0.44 s; every qew commit pays it. Add qew doctor [--fix], warn on init, document in CLAUDE.md.
