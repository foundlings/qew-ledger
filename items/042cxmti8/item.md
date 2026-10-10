id: 042cxmti8
kind: issue
title: Make `qew draft approve` report approved and skipped items and stay re-runnable
parent: 042cxmti7
needs: 
labels: area:drafts-plans
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew draft approve ITEM... [--tree] --quote Q` appends one `approved` event per draft it releases and must be
safe to run again. Required in the ledger model:
- Duplicate references on the command line (`A A`, or an alias and the full id) collapse to one target. Today two
  `approved` events are appended from one stale snapshot and the second is an illegal transition that makes
  `qew check` fail.
- A named item that is not a draft (already approved, claimed, completed) is skipped and reported when at least one
  other target remains; when nothing is left to approve the command exits 2 with `nothing to approve: X is not a
  draft`. This holds with and without `--tree`; today `--tree` over an already released plan silently exits 0
  with no output.
- A closed item named as a root is refused (exit 2) before any write; closed descendants are passed over.
- `--tree` visits each descendant once, follows `parent` edges only (not `needs`), and releases only drafts.
- Output lists `approved ID` and `skipped ID` lines; `--json` gives `{"approved": [...], "skipped": [...]}`.
- Every target is validated before the first event is written (all-or-nothing refusal for a bad root).

## Scenarios
1. Golden: approve one draft with a valid quote; exactly one `approved` event carrying the quote is appended, output `ID approved`. Prevents a release with no recorded words.
2. Tree golden: approve an epic with `--tree`; epic, its draft issue and that issue's draft task are approved once each, the already-approved sibling and the closed child get no event, JSON lists approved and skipped. Prevents skipped or double-written descendants.
3. Re-run after a partial failure: root already approved, children still drafts; `--tree` approves the children and exits 0. Prevents a rerun that refuses at the root and leaves children stuck.
4. Lone non-draft named: exit 2, `X is not a draft`, no event written. Prevents approving something that is not a draft.
5. Mixed list `A B` where B is already approved: A approved, B reported as skipped in text and JSON, exit 0. Prevents a one-item mistake aborting the batch.
6. `--tree` on a plan whose whole subtree is already approved: exit 2 `nothing to approve`. Prevents a silent no-op that looks like success.
7. Duplicate reference `A A` (and alias plus full id): one event, `qew check` still passes. Prevents a ledger that is invalid right after approval.
8. Closed root named: exit 2, nothing written. Prevents reviving discarded work.

## Reference coverage
Reference tests merged here: draft approve golden, tree approval, lone non-draft refused, already-approved skipped,
rerun of a tree after partial failure, closed draft refused, skipped issues named in human output (7 of 14 approve
tests). The reference lifecycle for drafts also sets the TREE_LIMIT of 1000 visited issues and the single-visit rule.

## Qew today
Covered: single approve (flow walk `approve_without_a_human_quote_is_refused` proves only the refusal, the ledger
walk helper approves in the golden walk), non-draft root refused when named alone (via the transition table, no
dedicated test), tree filtered to drafts, descendant set deduplicated.
Missing: skipped/approved reporting and JSON, nothing-to-approve refusal under `--tree`, duplicate-reference
collapse, closed-root refusal test, any dedicated tree walk. Reduced: error text does not name the next step.
