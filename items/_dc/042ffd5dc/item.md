id: 042ffd5dc
kind: epic
title: Item attachments: files, data structures and images owned by an item
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T23:11:50Z
evidence_absent: children: all 13 children finished
---
Owner request (relayed by Santa 2026-10-10, verbatim): 'I still need more in the qew files like data strucutes images etc like we have in phases, I don't like the -ledger format the way it works at the moment that it doesn't have directories to put down multiple files in items or have subdirectories, attachmenrs etc. qew has no way to record any of that and it desperately needs to. ... we probably need a qew migration for both ledgers aswell to the new format and then the important script later etc for the phases'.

Needs (foundlings, from docs/phases: ~1,190 md, 656 json receipts, 300 frozen source files, ~400 py/rs scripts, diagrams, data structures): (1) an item owns a directory of files and subdirectories; (2) attach/detach through qew, listed by show, referenced from the body by a stable relative path, validated by check, binary allowed, stated size limit; (3) part of history and evidence, committed with the item's events, survives item id migration; (4) defined mirror behaviour, never silently uploading binaries; (5) lossless migration command for both ledgers, dry-run first, check green before and after; (6) scriptable bulk attach from a manifest or create --from-file.

DESIGN WARNING (the base requirement is conflict-free merges, CLAUDE.md): a plain directory per item with files at fixed names conflicts in git when two machines replace or edit the same attachment (and binary conflicts are unresolvable by qew). Proposed shape that keeps merges conflict-free: attachment BYTES are immutable and content-addressed (one file per content hash, never edited in place), and the item NAMES them through events (attached/detached, name -> hash, last event by id wins), so two machines can never write the same path with different bytes. Item directory view (items/ID/NAME) is then derived, not stored. Decide in the first child draft before any code.

Children: 042-model (storage and events), attach commands, mirror behaviour, migration, bulk attach. All drafts: wait for the owner's words.
