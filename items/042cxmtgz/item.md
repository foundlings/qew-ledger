id: 042cxmtgz
kind: issue
title: Add `--edit` body authoring through VISUAL/EDITOR with safe temp-file handling
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: zrsmmolo
---
## Behaviour
`qew create --edit` and `qew set ITEM --edit` open the user's editor on an empty temp file in a private temp directory and use the result as the body. Rules: VISUAL then EDITOR; unset or blank refuses (exit 2) naming both variables; the command is shell-split (never run through a shell), a parse error refuses; non-zero editor exit refuses and writes nothing; an empty or whitespace-only body refuses; the temp dir is removed on every path; the body is never taken from anything but that file. `--body-file` (existing) refuses a symlink and an empty file; `qew set` with no change prints 'unchanged' and writes no event, and editing a closed item needs an explicit flag.

## Scenarios
- `edit_uses_the_editor_output_as_the_body`: fake editor script writes text; item body equals it.
- `missing_or_blank_editor_is_refused`: neither variable set: exit 2, ledger untouched.
- `failing_editor_or_empty_result_writes_nothing`: table: exit 1 editor, empty file.
- `body_file_symlink_is_refused`: prevents reading through a link.
- `set_with_no_change_writes_nothing`: no event file added.

## Reference coverage
No dedicated reference test file (the editor module is exercised through create/set walks outside this area). Edit module rules: set requires at least one change, closed targets need a flag, body-file symlink and empty refusals.

## Qew today
Missing: no `--edit`; `set_fields` returns 'unchanged' without writing (covered); body-file symlink refusal not present (verify `--body-file` read path).
