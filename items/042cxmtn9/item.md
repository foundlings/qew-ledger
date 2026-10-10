id: 042cxmtn9
kind: issue
title: Add `qew triage [--search TERMS]` to review drafts and items missing fields, with bodies and findings
parent: 042cxmtmt
needs: 042cxmtmu 042cxmtn3
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew triage` is the explicit read of unapproved text: it lists drafts and approved items lacking required planning fields (for the ledger: no label of any configured required group, empty body, or a task with no parent) with each item's title, body, and a `missing` list naming what is absent. `--search TERMS` narrows by title and body. Output carries `text_findings` per item and field (source `title` or `body`) and never rewrites the text. Triage is the only list-shaped read that prints unapproved bodies.

## Scenarios
- golden: a draft with a body matching the search and one without lists only the match, with `body` and `missing`. Prevents reviewers opening each draft.
- golden: two items missing different fields report different `missing` lists in sorted order. Prevents false completeness.
- adversary: an unapproved body full of instructions is printed as data with findings attached and is not present in `ready`, `prime` or hook context. Prevents injection through routine channels.
- golden: triage output is one object per line with schema_version. Prevents a contract split.

## Reference coverage
Reference read-suite walk: triage golden walk searches untriaged titles and bodies (1 test); triage text-findings walks map to text-scan-annotations.

## Qew today
Missing. No triage command.
