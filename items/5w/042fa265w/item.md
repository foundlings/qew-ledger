id: 042fa265w
kind: issue
title: Faster tests: build the starting ledger once and copy it per test
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T21:23:21Z
evidence: tkkxowprovqw yutlmsztzxnu
---
Owner 2026-10-09: reuse a pre-built ledger instead of rebuilding it per test, after the typing work merged. Measure first how much of the gate (about 4 minutes, 1150 tests) is World setup (git init of code and ledger repos, config, qew start-up subprocesses) and the big-ledger builds (large import, read scale); copy a template per test (no shared mutable state, no absolute paths baked into git or jj config) and build big ledgers once per module. Keep every walk's isolation; the gate must stay green and get measurably faster.
