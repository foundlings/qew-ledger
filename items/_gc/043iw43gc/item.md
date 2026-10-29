id: 043iw43gc
kind: issue
title: qew doctor reports a recrawling watchman watch and --fix resets it; a slow ledger commit warns once a day
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-29T01:07:23Z
evidence: e127cd7b 08944f5a
---
## Goal

doctor names a watch that recrawled (dropped file events make every jj snapshot wait), --fix runs watch-del and watch-project, and a ledger commit over 20 s prints one hint a day pointing at doctor
