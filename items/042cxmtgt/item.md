id: 042cxmtgt
kind: issue
title: Refuse reserved label namespaces and malformed labels in create, set and imports
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
Sync overwrites an issue's labels with the item's labels plus `qew:STATE`, `kind:KIND`, `priority:N`. A ledger label in those namespaces would either be shadowed or would spoof state on the forge (an item labelled `qew:approved` while still a draft). Refuse, with exit 2 and the word 'reserved', BEFORE any write, every label whose casefolded name starts with `qew:`, `kind:`, `priority:` or `author:` (the derived author label, see `item-author-derivation`), on `qew create --label`, `qew set --labels`, and every `--from-file` / `--import` item (dry-run validation too). Also refuse, with the same discipline: names longer than 50 characters, leading/trailing spaces, control characters or newlines, commas, empty names (whitespace and comma checks exist; extend). `qew check` flags the same labels already present in files (hand-edited or merged).

## Scenarios
- `create_refuses_each_reserved_label_before_any_write`: table of reserved names incl. mixed case; ledger unchanged on refusal.
- `set_refuses_reserved_labels_before_any_write`: `--labels` carrying a reserved name changes nothing and appends no event.
- `import_refuses_a_reserved_label_for_the_whole_file`: one bad item aborts the batch with no partial writes; applies to `--from-file` and `--import`.
- `malformed_label_names_are_refused`: table: 51 chars, edge spaces, newline, comma, empty.
- `check_flags_a_reserved_label_found_in_a_file`: merge-produced files cannot smuggle state.

## Reference coverage
Tests: reserved area walk (3: create refuses reserved area before any write, set refuses reserved add/remove before any write, apply refuses reserved plan area including dry run), area-ensure walk validation test (name table with 15 values, colour/description table). Spec: area names reserved by the tool.

## Qew today
Reduced. `cmd_items` only requires 'one word without commas'; nothing reserves `qew:`/`kind:`/`priority:` names; imports unvalidated for namespaces.
