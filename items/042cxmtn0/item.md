id: 042cxmtn0
kind: issue
title: Make every read refuse a partially readable ledger instead of listing what it could parse
parent: 042cxmtmt
needs: 
labels: area:read-side
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
Reads validate before printing: an unparseable item file, malformed event, unknown header key, duplicate id, or truncated header makes `list`, `ready`, `blocked`, `show`, `graph`, `prime`, `inbox` refuse (exit 1, nothing on stdout) naming the file. This is the ledger form of the reference rule that a truncated or incomplete page never produces a guessed answer. A single bad item must not be skipped silently, and a read must not hide the bad file by listing the rest.

## Scenarios
- refusal: one corrupt item file among ten good ones makes `qew list` and `qew ready` exit 1 with stdout empty and the file named. Prevents a partial ready queue.
- refusal: a dangling event directory for a missing item fails the read the same way. Prevents orphan history being ignored.
- golden: after the file is repaired the same commands succeed unchanged. Prevents a sticky cache of the failure.

## Reference coverage
Reference read-suite walks: list refuses incomplete pages; list refuses truncated blocker and assignee pages (2 tests). Reference ready walk truncated-blocker refusal and prime nested-pagination refusal map here (2 tests). Forge pagination itself is dropped.

## Qew today
Partially covered by `qew check` tests (unknown key, malformed event) which exercise `check`, not the read commands; hook session-start silence on unreadable ledger is covered. No walk shows read commands refuse.
