id: 042cxmtiv
kind: issue
title: Decide `qew apply` versus `create --from-file` and align help, README and specs
parent: 042cxmti7
needs: 042cxmtiq
labels: area:drafts-plans
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: nkqlvnso
---
## Behaviour
Decide whether the plan-file workflow is a separate `qew apply FILE [--draft] [--dry-run] [--json]` or stays
`create --from-file`; either way there is one documented path. Add to the repo: a plan-files section in
`docs/specs/commands.md` (or a new `docs/specs/plan-files.md`) stating fields, rules, dry-run, rerun marker and
draft rule; README text for implemented behaviour only; a `--help` line for every flag and the command in a group
of the `qew --help` epilog. A walk fails when a flag has no help line or is missing from README or spec. Add the
drafts rules (human quote only, tree approval, revert guards, no force flag) as a short `docs/specs/drafts.md`.
Apply field names are English and follow the header keys (`needs`, `parent`, `labels`, `priority`, `ref`).

## Scenarios
1. Help walk: every apply/draft/plan flag has a help line, README and spec mention. Prevents undocumented flags.
2. A plan file example in the spec is parsed by the real validator in a test. Prevents a spec that rots.

## Reference coverage
Reference docs: plan-files.md (fields, dry-run, checkpoint, provenance marker) and drafts.md (model, commands,
board, plan pull requests, pull request flow). Pull request and board sections belong to other areas.

## Qew today
`docs/specs/commands.md` documents `draft` and `create --from-file`; there is no plan-file or drafts spec.
