id: 042cxmtid
kind: issue
title: Give `qew draft list` a parent filter, stable shape and a walk
parent: 042cxmti7
needs: 
labels: area:drafts-plans
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew draft list [--parent ID] [--json]` shows open drafts (state draft; closed, approved and claimed excluded)
ordered by priority then id, each with kind and parent so a plan and its children are legible. `--parent`
restricts to drafts whose `parent` is that item (direct children). Scope follows the ledger: a mirror target with
`select` does not change what the ledger lists. The list reads only item and event files, no network.

## Scenarios
1. Golden: an epic draft and a task draft under it appear with kind and parent in text and JSON. Prevents a draft no read can find.
2. A closed draft and an approved item are not listed. Prevents stale rows hiding the real review queue.
3. `--parent EPIC` lists only that epic's direct draft children. Prevents reviewing unrelated drafts when releasing one plan.
4. Alias parent reference resolves; unknown parent exits 2. Prevents a typo producing an empty, plausible list.

## Reference coverage
Reference draft-read tests: draft list shows open drafts with type and parent, ignores closed or non-draft,
only under a parent, overlay mode asks only for managed drafts (4 of 8). The overlay variant is dropped: it
exists to filter GitHub label scope.

## Qew today
Implemented without `--parent`; no test at all for `draft list`. Text row already shows kind; JSON has parent.
