id: 042cxmtn7
kind: issue
title: Complete `qew draft list`: parent scope, type, closed excluded, drafts findable by every read
parent: 042cxmtmt
needs: 042cxmtmu
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew draft list` shows open drafts with kind, parent, priority and title, sorted parent-first then id, with `--parent ID` to scope to one epic and `--json`. Closed or approved items never appear. The reference failure to prevent is a draft no read can find: in the ledger drafts must be reachable by `draft list`, `list --state draft`, `show` and `triage` and never by `ready` or `prime`.

## Scenarios
- golden: draft list shows each draft with kind and parent, epics before their children. Prevents orphaned ideas.
- golden: a closed draft and an approved item do not appear. Prevents noise.
- golden: `--parent E` lists only drafts under E. Prevents scanning the whole backlog.
- adversary: drafts never appear in `ready` or in the session-start context, while a count of drafts does. Prevents unapproved work being offered.

## Reference coverage
Reference draft-read walks: draft list shows open drafts with type and parent; ignores closed or non-draft; only under a parent; overlay-mode query (forge-only, dropped) (3 mapped + 1 dropped).

## Qew today
Reduced. `qew draft list` exists (cmd_draft) but there is no `--parent`, no kind/parent columns asserted, and no dedicated walk.
