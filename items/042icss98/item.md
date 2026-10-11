id: 042icss98
kind: issue
title: Write commands scan the whole working copy: jj commit, the recovery check and the write-session fetch cost seconds on a 165k-file ledger
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-11T10:02:52Z
---
Measured on the live foundlings ledger (6.9.1): reads are 5 s, writes still run 'jj commit' (a snapshot of every file), the recovery scan (jj diff --summary) at session start, and a fetch+merge. Goal: a write costs about a read plus the commit. Ideas to evaluate: skip the recovery scan when .qew/writing is absent (as reads now do), jj --ignore-working-copy where a snapshot is not needed, commit only the written paths without a full snapshot, measure each step with QEW_TRACE on a copy-on-write ledger copy under load. Acceptance: write command wall time on the foundlings copy within ~2 s of a read.
