id: 042cxmtn4
kind: issue
title: Add the explicit body-inspection read: `qew list --bodies` and `qew show` as the only body readers
parent: 042cxmtmt
needs: 042cxmtmy 042cxmtn3
labels: area:read-side
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
Routine reads (`ready`, `prime`, hook context) never emit item bodies; bodies appear only via `qew show ITEM` or `qew list --bodies`, both explicit inspection actions, and only for approved work in `--bodies` (drafts via `show` or `triage`). Output is annotated with text findings and never rewritten.

## Scenarios
- golden: `qew list --bodies --json` includes `body` for approved items and nothing for drafts. Prevents routine bulk reads exposing unapproved text.
- adversary: `qew ready --json` and `qew prime` on an item whose body holds an instruction never contain the body. Prevents prompt injection through routine context.

## Reference coverage
Reference security spec section on explicit body inspection, reference read-suite list golden walk (1 test shares it).

## Qew today
Missing. `qew show` prints the body; list has no body option; no walk asserts bodies are absent from ready/prime.
