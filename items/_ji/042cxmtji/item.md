id: 042cxmtji
kind: issue
title: Pin each agent's non-blocking and blocking output shape for every hook event
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: utnmomos
---
## Behaviour
Each agent receives only its documented shape: Claude and Codex `hookSpecificOutput` with the event name; Cursor `{permission, user_message, agent_message}` (explicit allow always) and `{additional_context}` at session start, nothing for the after-shell event; opencode plain text with exit 2 for deny and no JSON braces.

## Scenarios
- Same bypass command sent to all four agents: four shapes asserted, Cursor quiet command yields exactly `{permission: allow}`. Prevents invalid output, which blocks the agent.
- Session start per agent: shapes asserted (opencode has no session-start entry).
- Post-tool per agent: Cursor prints nothing, opencode plain text, Claude/Codex PostToolUse context.

## Reference coverage
3 tests (each agent gets its own shape; cursor runs landing and prints nothing; opencode plain text).

## Qew today
Covered for deny shapes (cursor and opencode deny walk). Missing: post-tool shapes per agent and the quiet-Cursor allow row.
