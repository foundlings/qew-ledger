id: 042cxmtim
kind: issue
title: Prove graph algorithms stay iterative on very long chains
parent: 042cxmti7
needs: 
labels: area:drafts-plans
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: kuzrwqwt
---
## Behaviour
Cycle detection, readiness, `blocked`, `check` and the apply validation must not recurse per node. A 3000-link
dependency chain must be accepted and a 3000-node cycle still reported, with no traceback and in bounded time.
`find_cycles` is already iterative; the ordering and blockers helpers are linear. Pin it.

## Scenarios
1. Create/load a 3000-item chain through a plan file and run `qew check`, `qew ready`, `qew blocked`, `qew graph`: all exit 0, no traceback. Prevents a recursive cycle search overflowing on real plans.
2. The same chain closed into a ring reports a cycle (exit 1) without a traceback. Prevents the opposite failure.

## Reference coverage
Reference apply seam walk: long chain without recursion error (1 of 14).

## Qew today
Implementation is iterative; no test.
