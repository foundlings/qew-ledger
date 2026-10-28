id: 042cxmtj9
kind: issue
title: Pin hook install/remove ownership: foreign entries kept, only Qew's own old entries dropped, per agent
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: wlskzyqr
---
## Behaviour
For each agent install and remove touch only Qew-owned entries. Foreign entries in the same event list, unrelated top-level keys (permissions, theme, `version`) and unrelated plugin files survive byte-for-byte in meaning. Qew's own earlier entries (earlier shell-hook generation, `qew prime`, exec-form and unguarded command strings) are replaced on install and deleted on remove. When removal empties an event list or the hooks node the empty container is pruned; Cursor keeps `version: 1`.

## Scenarios
- Claude: foreign PreToolUse group plus foreign SessionStart plus Qew's old entry; install, rerun (`unchanged`), remove restores the foreign-only file exactly. Prevents clobbering a teammate's hooks.
- Codex: same walk against `.codex/hooks.json`, including pruning to `{hooks: {PreToolUse: [foreign]}}` after remove.
- Cursor: foreign `afterFileEdit` entry kept, old Qew `sessionStart` entry dropped, `version: 1` retained on remove.
- opencode: unrelated `keep.js` untouched; Qew's earlier plugin file is deleted only when it carries Qew's marker; an unmarked file with the old name is left alone (install still succeeds).
- Remove-only on a file holding just Qew's leftover entry leaves `{}` (Claude). Prevents a stale entry surviving remove.

## Reference coverage
Maps tests: claude install/keeps others, claude installs without session-start (inverted in qew: qew installs SessionStart on purpose), claude remove deletes leftover prime entry, codex install+trust, cursor install, opencode replaces only owned plugin, opencode unowned prime plugin. About 7 tests merged into 5 scenarios.

## Qew today
Reduced. The hook v1 walk has one combined foreign-entries scenario and one opencode scenario; Codex and Cursor pruning, the all-empty `{}` result and the unowned old-name plugin are not pinned separately.
