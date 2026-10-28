id: 042cxmtgu
kind: issue
title: Make label creation during sync create-only and neutral, on every backend
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: ynxmurrs
---
## Behaviour
The reference's `area ensure` command is dropped (labels live in item headers, forges get them from sync) but its two guarantees remain for sync: a label that already exists on the forge is NEVER recoloured, re-described or deleted by sync (a team tuned it), and a label sync must create gets a neutral colour (`EDEDED`) and a short fixed description. After creating missing labels the backend confirms the labels exist; one that did not persist is a typed indeterminate failure of that item, not a silent success.

## Scenarios
- `existing_label_keeps_color_and_description`: pre-seeded label with a custom colour survives a sync that applies it; prevents retuning.
- `missing_label_is_created_neutral_exactly_once`: a second sync issues no label create.
- `label_creation_that_does_not_persist_fails_the_item`: fake drops the create: item reported failed; prevents a phantom label.

## Reference coverage
Tests (area ensure walk, 6): missing label created without force and verified, existing label never overwritten even with other options, defaults give a neutral colour and description, reserved and malformed names refused (in `labels-reserved-namespaces`), malformed colour or description refused (dropped with the command), creation that does not persist is indeterminate.

## Qew today
Partly covered: Forgejo creates `#ededed` labels (spec); GitHub creates labels implicitly on issue write; GitLab labels created for boards. No walk pins 'never overwrite'.
