id: 044ak8896
kind: issue
title: pr merge --check: batch preflight runs per-PR loads and checks sequentially
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-11-11T06:58:58Z
evidence: xmtnyvok ytqqoqps
---
## Where

src/qew/pr_batch.py (run, _heads), src/qew/cmd_pr.py (merge_check, load)

## Problem

qew pr merge N1..N8 --check takes 75-106 s in the foundlings merge gate (about 10 s per PR); every other gate setup step is under 2 s. pr_batch.run checks PRs in a plain list comprehension over merge_check, one PR after another. Each merge_check calls load(), which builds a new ledger handle and a fresh ledger.snapshot() plus a forge read; _heads() already loops the same PRs through load() first, so an 8-PR batch takes 16 ledger snapshots, all serial.

## Fix

Load the ledger snapshot once per batch and share it across _heads and every merge_check; read the pull requests from the forge concurrently (ThreadPoolExecutor, as ledger_store/snapshot_cache already do). Keep refusal order and exit codes identical to the serial run.

## Done when

A test proves one snapshot load per batch and concurrent forge reads; refusals and exit codes unchanged; a release ships and an 8-PR --check runs in a few seconds.
