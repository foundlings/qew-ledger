id: 042cxmtnb
kind: issue
title: Prove `qew check`, `ready` and `blocked` stay linear on big and deep graphs
parent: 042cxmtmt
needs: 
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: lrxtvrzrqrow
---
## Behaviour
Graph derivation must be linear in nodes plus edges, iterative (no recursion limit), and independent of path counts. The cycle finder is iterative already; what is unproven is behaviour on adversarial shapes. A layered diamond with 40 layers has 2^40 paths, a 3000-long need chain overflows a recursive search, and a 5000-item ledger must still read fast from files with no index (the ledger spec decided no index is built).

## Scenarios
- adversary: 40 layers of two-node diamonds validate in under one second with no cycle reported. Prevents path-enumeration blowups.
- adversary: a chain of 3000 needs passes `qew check` and `qew ready` without a recursion error. Prevents a crash on deep graphs.
- adversary: a cycle inside a large acyclic graph is still reported with its path (A -> B -> A). Prevents the performance fix hiding cycles.
- golden: a ledger of 5000 items answers `qew ready` within a bounded time budget asserted in the test. Prevents the no-index decision silently regressing.

## Reference coverage
Reference model-output walks: diamond layers linear time; long chain without recursion error; graph check golden clean DAG; graph check reports cycles (4 tests; cycle detection partially covered).

## Qew today
Reduced. `find_cycles` is iterative, and `test_a_dependency_cycle_fails` covers a 2-node cycle. No scale or adversarial-shape test.
