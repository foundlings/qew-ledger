id: 042cxmtjc
kind: issue
title: Record why exec-form hook commands are replaced by the guarded single string
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: rqvnrumn
---
## Behaviour
Spec-only: docs/specs/hooks.md already says Claude and Codex entries are one guarded `command` string with no `args`. Add the explicit decision that the reference's exec-form entry (command plus args) is rejected because older agent versions mis-handle it and a bare missing binary would exit 2 and block every shell call.

## Scenarios
None new; the guarded-command walks (no args key, missing qew fails open, real refusal still blocks) already cover it.

## Reference coverage
1 test (claude hook command runs the tool in exec form) mapped to those walks.

## Qew today
Covered by the guarded command walks. Only the written decision is optional.
