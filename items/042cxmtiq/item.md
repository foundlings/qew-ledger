id: 042cxmtiq
kind: issue
title: Validate a whole work-plan file before writing anything
parent: 042cxmti7
needs: 
labels: area:drafts-plans
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: zzrmsqkq
---
## Behaviour
The reference accepts one JSON object per line and rejects the entire plan before the first write. Ledger form:
`qew create --from-file` (or a dedicated `qew apply FILE`, decided in apply-command-surface) must accept JSONL as
well as one object/array and validate everything first. Rules, all exit 2 with the line number and no file written:
- file must be a regular UTF-8 file, not a symlink; empty or no work items refused; blank lines ignored;
- invalid JSON, a non-object line, an **unknown field** (today silently ignored), wrong types, blank title, bad
  kind, non-integer or negative priority;
- local `ref`s unique (today a duplicate `ref` silently overwrites the first), and an explicit `ref` may not
  equal another entry's generated key `line-N`;
- `@ref` references resolve in any order (today a forward reference fails as unknown), and a dangling one is
  refused;
- `needs`/`parent` cycles among new items and through existing items are rejected, nesting rules enforced,
  iterative so a 3000-link chain is fine;
- imported `id` collisions refused (already true).

## Scenarios
1. Valid JSONL of an epic and two tasks is accepted; same content as a JSON array is identical. Prevents format-dependent behaviour.
2. Unknown field on line 2 refused naming `line 2` and the field, zero items written. Prevents typos (`need`, `blocked-by`) silently dropping a dependency.
3. Duplicate `ref`, and `ref: line-1` colliding with an anonymous first entry (both orders) refused. Prevents a skipped entry and mis-resolved references.
4. Forward reference (`needs: ["@b"]` before b is defined) works; dangling reference refused. Prevents order-dependent plans.
5. Local cycle a needs b needs a refused before any write; cycle through an existing item refused. Prevents cycles from files.
6. Symlinked plan file, non-UTF-8 bytes, invalid JSON on line 3, empty plan each refused. Prevents reading something other than the reviewed file.
7. Priority `P1` or `-1` refused with the field named. Prevents a header that fails `check` later.

## Reference coverage
Reference apply tests merged: cycle rejected before writes, explicit id colliding with a generated line key (both
orders), dry-run golden walk validation, long chain (shared with graph-deep-chains) - 3 of 14. Plan-files spec:
unknown fields, invalid values, dangling local refs and cycles reject the whole plan; `id` unique; `line-N` keys.

## Qew today
Reduced: `create --from-file` takes JSON object/array only, ignores unknown keys, lets a duplicate `ref` overwrite, resolves `@ref` only to earlier entries, no cycle, nesting or symlink checks beyond the id syntax.
