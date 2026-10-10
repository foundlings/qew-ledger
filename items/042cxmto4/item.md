id: 042cxmto4
kind: issue
title: jj push integration without git hooks
parent: 042cxmto2
needs: 042cxmto3
labels: area:vcs-hook
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
jj has no pre-push hook: provide `qew hook vcs-check` for scripts and the agent PreToolUse guard on `jj git push`.
Scenarios:
- refusal: jj git push of a change citing an unevidenced id is blocked by the agent guard
