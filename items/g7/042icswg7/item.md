id: 042icswg7
kind: issue
title: Large git ledgers: set core.untrackedCache at creation and on open (fsmonitor and splitIndex measured, not recommended)
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-11T10:02:56Z
evidence: qrqsktuo rykoqzkq
---
Measured on a copy of foundlings-ledger (165k files, git 2.54, load 6-15): git status 1.8-2.2 s baseline, 0.48-0.57 s with core.untrackedCache=true (verified safe by git update-index --test-untracked-cache), 2.4-2.9 s with core.fsmonitor=true (6.4 s the first time, a daemon per checkout, slower than untrackedCache alone), splitIndex: index is only 2.7 MB so the write saving is small and unmeasured. jj colocated ledgers do not use the git index for qew's operations (jj snapshots its own working copy), so these settings only help ledgers whose vcs is git. Proposal: set core.untrackedCache=true when qew creates or opens a git ledger (idempotent, no schema bump, same place as the .qew/ exclusion). Waiting for the owner's decision before building; also decide fsmonitor/splitIndex.
