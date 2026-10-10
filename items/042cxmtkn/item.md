id: 042cxmtkn
kind: issue
title: Support a structured body and editor-authored body on create
parent: 042cxmtjw
needs: 
labels: area:lifecycle
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
Reference `create` composes the body from `--where`, `--problem`/`--goal`, `--fix`/`--approach`, `--done-when` (rendered as headed sections), or reads `--body-file`, or opens `--edit`. `--problem` and `--goal` are exclusive, `--fix` and `--approach` are exclusive, and structured fields, `--body-file` and `--edit` are mutually exclusive (exit 2, before any write). The editor command is tokenized and executed directly, never through a shell. `--done-when` could become child `task` items (the ledger keeps tasks as items, not checkboxes) or stay a body section. YAGNI check before building: qew already has `--body` and `--body-file`; implement only if agents actually need the structure.

## Scenarios
- golden: structured flags produce the sectioned body (prevents: free-form bodies that omit done-when)
- ambiguous framing (`--problem` with `--goal`) or body plus structured flag: exit 2, zero files
- editor value `python editor.py ; touch marker`: runs as argv, marker file never created (prevents: shell injection through EDITOR)

## Reference coverage
3 reference test function(s): `test_create_golden_walk_composes_approved_work`, `test_create_seam_walk_refuses_ambiguous_body`, `test_create_editor_golden_walk_uses_editor_body_without_a_shell`

## Qew today
Missing (only `--body`, `--body-file`, `-` for stdin).
