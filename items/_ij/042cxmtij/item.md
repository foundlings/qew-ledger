id: 042cxmtij
kind: issue
title: Add `qew block` and `qew unblock` for incremental, idempotent dependency edits
parent: 042cxmti7
needs: 042cxmtii
labels: area:drafts-plans
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: tutktyws
---
## Behaviour
`qew block ITEM --on BLOCKER` appends BLOCKER to ITEM's `needs`; `qew unblock ITEM --from BLOCKER` removes it.
Both resolve aliases, validate the whole graph first (graph-write-validation), are no-ops when the edge already
is (not) there (exit 0, `unchanged`), write one `field` audit event, and read the result back. A closed ITEM needs
`--closed`. Rationale: `set --needs` replaces the full list, so two writers adding different blockers rewrite the
same header line and collide; the edge commands make the change minimal and the audit event precise. Update
`--help`, README and `docs/specs/commands.md` together (the three-place rule).

## Scenarios
1. Golden block: edge added, item moves from ready to blocked, output and `--json` name both ids. Prevents a dependency that does not gate readiness.
2. Block twice is a no-op (no second event). Prevents audit noise and redundant rewrites.
3. Block that would close a cycle refused before write; self block refused. Prevents corrupt graphs.
4. Golden unblock removes the edge and the item becomes ready; unblock of an absent edge is a no-op. Prevents wrongly resurrecting needs.
5. Closed item: block and unblock refuse without `--closed`, work with it. Prevents silent edits of finished work.

## Reference coverage
Reference graph-write tests: block golden walk adds and verifies edge, block seam walk refuses transitive cycle,
unblock golden walk removes and verifies edge, block refusal walk requires closed override, unblock golden walk allows
explicit closed target (5 of 26; the cycle one is shared with graph-write-validation).

## Qew today
Missing: no `block`/`unblock` commands; only the replace-all `set --needs`.
