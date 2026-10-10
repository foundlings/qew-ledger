id: 042g20y2k
kind: issue
title: Item files live inside their directory: items/ID/item.md, schema_version 3
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T06:33:53Z
---
Owner (this session): the item files themselves go into the item directories and no longer carry the ID in the file name; only the directory has the ID.

Layout: items/<ID>/item.md (header + body), attachments stay items/<ID>/attachments/. events/<ID>/ and mirrors/<ID>/ already are per-ID directories and stay. schema_version 3.

Plan (phases, each RED then GREEN):
1. Path seam: one function in ledger_store (item_path(id), item_ids() = directories holding item.md) and every reader/writer goes through it: ledger_store, ledger_aliases (scan/refresh), ledger_check (orphans, items dir), id_migration (rename/discard now move directories), cmd_transfer (export/import), cmd_forgeio, ledger_invariants, ledger_conflicts, cmd_conflicts, attachments, attach_batch, comment_batch, attachment_links. qew reads ONE layout per schema: schema 3 only; no dual-read at runtime.
2. qew migrate-layout moves 1 or 2 to 3: git/jj mv items/ID.md to items/ID/item.md for every item (aliases and superseded leftovers too), bumps schema_version, one commit; needs qew check green before and after and no claim held by another login; refuses with a clear message if items/ID.md and items/ID/item.md both exist. All other commands refuse a schema 1 or 2 ledger naming migrate-layout. qew init writes 3. An older qew refuses schema 3 (already strict).
3. Tests: the harness and every walk that writes or reads items/*.md move to the seam (about 56 test files touch the path); migration walk checks every item's bytes are identical at the new path, ids/aliases/mirrors/events untouched, check green, rerun is a no-op.
4. Migrate qew-ledger, then Santa migrates foundlings-ledger. minimum_version bump for both.

Risks to state to the owner: it is a rename of every item file (368 here, about 2000 in foundlings): a clone with an unpushed edit to items/ID.md will conflict with the move in jj (no rename tracking) and may in git; do it with all writers pushed and quiet (the claim check covers claims, not edits). Conflict-free merges stay intact afterwards (still one file per item, per event, per mirror). Name question: item.md vs README.md vs the ID-free fixed name the owner prefers.
