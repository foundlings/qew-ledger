id: 042cxmtir
kind: issue
title: Add `--dry-run` that prints the operations a plan file would perform
parent: 042cxmti7
needs: 042cxmtiq
labels: area:drafts-plans status:Backlog
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`--dry-run` runs the full validation, performs no write and no network call, and prints the operation list in
apply order: `create` (id/ref, title, kind, `draft: true` when it will be a draft), `parent`, `need` edges. JSON has
`schema_version: 1`, `plan_sha256` (digest of the raw bytes) and `operations`. Exit 0 when valid, 2 otherwise. A
stale partial state from an earlier run is checked (see apply-idempotent-rerun) but not modified.

## Scenarios
1. Golden dry-run of epic plus task with a parent, an existing-item need and a local need: exact operation list, ledger untouched (file listing identical). Prevents reviewing a plan by applying it.
2. Dry-run of a draft-filed plan shows `draft: true` on each create. Prevents surprise releases.
3. Dry-run of an invalid plan exits 2 with the same message as a real run. Prevents a dry-run that passes what apply refuses.

## Reference coverage
Reference apply tests: dry-run golden walk validates without GitHub calls, dry-run with draft writes nothing and says
draft (the draft half of apply-draft walk) - 2 of 14 + 1 of 3. The two throttle dry-run/validation tests are dropped
(see dropped).

## Qew today
Missing: `create` has no dry-run mode.
