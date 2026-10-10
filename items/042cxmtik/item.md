id: 042cxmtik
kind: issue
title: Extend `qew set` with additive labels, body files and kind changes, verified on read-back
parent: 042cxmti7
needs: 042cxmtii
labels: area:drafts-plans
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: pvppxykq
---
## Behaviour
`set` today replaces `labels` wholesale and the body only from a literal string. Reference `set` covers title, body
from file, priority, type, add/remove area, parent, each verified afterwards. Ledger equivalent: `--add-label` /
`--remove-label` (labels stay one word, no commas), `--body-file F|-`, `--kind` (revalidated against nesting
rules of graph-write-validation), `--priority` non-negative integer, and one `field` event per changed key. After the
write the item is re-parsed and compared; a mismatch is exit 3. Contradictory flags (`--labels` with add/remove)
are exit 2 before any call.

## Scenarios
1. Golden: change title, body from file, priority, kind, add and remove a label and the parent in one call; one audit event per key, `--json` reports changed. Prevents partial or unaudited edits.
2. Add/remove label are idempotent and leave other labels. Prevents two writers clobbering each other's labels.
3. `--kind task` on an epic that has children is refused. Prevents orphaning the tree.
4. `--labels` combined with `--add-label` refused. Prevents ambiguous intent.

## Reference coverage
Reference graph-write set golden walk (1 of 26). The needs-approval set tests (3) are dropped.

## Qew today
Reduced: `set` has title, parent, needs, labels (replace), priority, body (literal). No additive labels, body file, kind change or read-back.
