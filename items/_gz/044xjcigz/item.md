id: 044xjcigz
kind: issue
title: qew pr open creates the forge PR before taking the ledger lock, leaving orphans
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T04:41:53Z
evidence: yxkvptvm yumkkuzu krvywlut
---
## Where

src/qew/cmd_pr*.py (pr open), replication write session

## Problem

pr open creates the forge PR and declaration block, then writes the record under the ledger lock. Under contention the lock wait times out (exit 3) and the PR is orphaned: later pr link/ready/sync refuse it as not recorded in the ledger (foundlings #8159 #8161 #8163 #8165 #8167 #8169). Secondary: some verbs report waited 60s although QEW_REPO_LOCK_WAIT_S=300.

## Fix

Take the ledger lock before creating the forge PR, or retry the record write against the created PR; let pr open --head B adopt an existing open PR for that head; make every verb honor QEW_REPO_LOCK_WAIT_S.

## Done when

A walk with a held lock shows pr open leaves no orphan and a rerun adopts the PR; the lock-wait env var is honored in every verb.
