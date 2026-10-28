id: 042cxmtnc
kind: issue
title: Extend `qew check` with advisory findings: suspicious titles, epic claimed, JSON report
parent: 042cxmtmt
needs: 042cxmtn1 042cxmtmu
labels: area:read-side
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: lkwvxzzuxwpk
---
## Behaviour
`qew check` stays fatal on schema, cycle, dangling and illegal-state problems and gains advisory (non-fatal) notes shaped like the reference `graph check` report: `cycles`, `contradictions` (an epic that is claimed, an item both approved and with a draft marker label, a priority outside the allowed range), and `text_findings` per item and field. `--json` prints `{valid, cycles, contradictions, text_findings, schema_version}`. Exit 1 only for fatal problems; advisory notes alone exit 0.

## Scenarios
- golden: a clean ledger reports `valid: true` and empty lists. Prevents false alarms.
- adversary: an item title carrying a right-to-left override and a two-node cycle yields both `cycles` and `text_findings` in one JSON report and exit 1. Prevents hidden-text items passing health checks.
- golden: only advisory findings present exits 0 with the findings listed. Prevents blocking work on a style warning.

## Reference coverage
Reference model-output walks: graph check reports cycles, contradictions and unicode findings; golden clean DAG (2 tests). Multiple-priority and multiple-type contradictions are label-vocabulary artifacts and dropped (priority and kind are single header fields).

## Qew today
Reduced. `qew check` prints text problems and notes only; no JSON, no advisory text findings, no claimed-epic contradiction.
