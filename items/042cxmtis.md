id: 042cxmtis
kind: issue
title: Make plan application re-runnable: adopt already-created items instead of duplicating
parent: 042cxmti7
needs: 042cxmtiq
labels: area:drafts-plans status:Backlog
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
GitHub writes are not atomic, so the reference keeps a checkpoint file, a plan digest and a provenance marker per
entry. The ledger is the source of truth, so no separate state file is needed: each created item's first event
carries `plan` (sha256 of the plan bytes) and `key` (the entry's ref or `line-N`). Re-running the same plan:
- finds items by `(plan, key)` in event files and adopts them instead of creating again; edges and events missing
  from a crashed first run (item file written, no events yet; `check` reports `no events`) are completed;
- two items with the same marker (ambiguous) is exit 2 before any creation, naming both;
- an item with the same key but a different plan digest (edited plan) is refused as `plan revision mismatch`,
  naming the items, so an edit cannot silently duplicate or overwrite;
- the marker is accepted only in its canonical form (64 hex digest + key); anything else in a body or event is not
  provenance.
Result JSON lists `created` key -> id.

## Scenarios
1. Interrupted run (fault after the first item) then identical rerun: no duplicate, final ledger equals an uninterrupted run, `qew check` clean. Prevents duplicate work after a crash.
2. Crash between item file and event: rerun adopts the item and writes the missing event. Prevents orphan item files that fail check.
3. Two items carry the same marker: rerun exit 2 `ambiguous`, nothing created. Prevents linking the wrong work.
4. Edited plan (new digest) run over items from the old digest: exit 2 naming them. Prevents silent duplication.
5. A body or title containing marker-like text is not adopted (only canonical event data counts). Prevents an attacker-supplied lookalike hijacking a key.

## Reference coverage
Reference apply tests: golden walk resumes without duplicate creation, resume after lost checkpoint adopts marked
issue without duplicate, resume refuses ambiguous marker matches before creating, resume refuses checkpoint when
completed parent write is missing (maps to revision mismatch / missing edge completion), resume refuses noncanonical
provenance marker - 5 of 14. The checkpoint state file, the live-GitHub verification of checkpointed parents, blockers,
campaign and project, and per-write checkpointing are dropped (ledger is the state).

## Qew today
Missing: `create --from-file` generates fresh ids every run; a rerun after a crash duplicates every item.
