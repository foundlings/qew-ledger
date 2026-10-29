id: 042cxmtmm
kind: issue
title: Add `qew pr merge --admin --reason TEXT`: bypass the check rule only
parent: 042cxmtm4
needs: 042cxmtmg
labels: area:pull-requests
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: lkkplpsu
---
## Behaviour
`--admin` merges past branch protection (pending/failing check gate) and prints `admin merge: REASON`; `--reason` is required with it (exit 2 before any call) and is exit 2 without it. It never bypasses the draft, conflict, checklist, covered-draft or ownership rules. The reason is recorded as a ledger `field`-style audit comment on the covered items so the bypass is reviewable. Forges without a bypass raise `Unsupported`.

## Scenarios
- admin without reason: exit 2, zero calls. Prevents: silent bypass.
- admin skips pending checks, prints reason, merge call carries the bypass. Prevents: blocked emergency docs-only merge.
- admin still refuses draft, open checklist items, conflicts, covered draft, other author: each exit 2/3, zero merges. Prevents: admin as a master key.
- contradictory options (`--auto --admin`, `--reason` alone): exit 2 before any call.

## Reference coverage
Reference pr merge walk file: admin needs reason, admin skips check rule, admin still refuses drafts, admin refuses every readiness rule, contradictory options. 5 test functions.

## Qew today
Missing: no flag; qew's own rules say `--admin` is part of the working flow.
