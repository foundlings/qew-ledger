id: 042cxmtit
kind: issue
title: Apply plan files with a per-item quote and a draft-by-default or --draft release rule
parent: 042cxmti7
needs: 042cxmtiq 042cxmtig
labels: area:drafts-plans
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
Reference: every line carries its own `quote` (validated before any write), `approved: true` says the quote also
authorizes starting, and `--draft` files every item as a draft and refuses a line with `approved: true`. Ledger
mapping: an entry with a valid `quote` is filed approved (as `create --quote` does) unless the run is `--draft`,
which files everything `drafted` and refuses any entry carrying `approved: true` (exit 2 naming `--draft`) before
any write. Entries with no quote are drafts. One quote at the top level (`--quote`) is a default for entries without
their own. Release of a draft plan is `qew draft approve EPIC --tree --quote Q`. Epic `approved` needs no
special case in the ledger (an approved epic is simply not ready). The recorded quote is the item's own.

## Scenarios
1. Plan of an epic and a task filed with `--draft`: both `drafted`, none approved, none in `ready`. Prevents a draft plan leaking into ready work.
2. A line with `approved: true` under `--draft` is refused naming `--draft`, nothing written. Prevents an approved line quietly winning.
3. Two entries with different quotes: each approved event carries its own quote; an entry without a quote is a draft. Prevents attributing one human's words to another's request.
4. A bad quote on line 2 refused with `line 2` before line 1 is written. Prevents a half-written plan.

## Reference coverage
Reference apply-draft tests: every created issue and epic is a draft, an approved line is refused under draft before
any write (2 of 3; dry-run draft is in apply-dry-run). Requester-quote tests: apply refuses an item without its own
quote before any write, apply renders each item quote and gates unapproved work (the quote half; the gate half is
dropped) - 2 of 9.

## Qew today
Reduced: one `--quote` for the whole file, no per-item `quote`/`approved`, no `--draft` flag (drafts are the default only when no quote is given).
