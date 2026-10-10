id: 042cxmtja
kind: issue
title: Refuse malformed agent config without rewriting, with a named reason per agent
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
Install and remove fail with exit 2 and leave the file byte-identical when the agent config has the wrong shape: Claude event node not a list (`PreToolUse must be a list`, also SessionStart/PostToolUse), Codex `hooks` not an object, Cursor `version` not 1 (`unsupported Cursor hooks version`), unparseable JSON, opencode target present without Qew's marker (`not managed by Qew`). Messages name the file and the offending node.

## Scenarios
- One refusal walk per agent comparing file bytes before and after. Prevents a half-valid config being repaired destructively.
- Unmarked opencode `qew-hooks.js` stays untouched and exit 2.

## Reference coverage
4 tests (claude malformed list, codex malformed object, cursor version, opencode unowned target).

## Qew today
Reduced. One malformed-config scenario exists in the hook v1 walk (generic); per-agent shapes and the Cursor version refusal need their own named walks.
