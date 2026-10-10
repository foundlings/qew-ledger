id: 042cxmtjj
kind: issue
title: Never fail the agent on malformed or hostile hook input
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
Every hook event exits 0 with empty output (explicit allow for Cursor) on empty stdin, non-JSON, JSON that is not an object, non-string command, non-object tool_input, a missing qew ledger or an internal exception. Only a deliberate refusal is non-silent.

## Scenarios
- Five malformed payloads per event: exit 0, empty output, no ledger write. Prevents a hook crash breaking every shell call.
- Unreadable or unparseable ledger: session-start and post-tool silent (covered for session-start).
- Injected exception inside the handler: swallowed in `cmd_hook.run` only; install/remove remain loud.

## Reference coverage
1 test (malformed input never fails the agent).

## Qew today
Covered (malformed payloads never fail the agent). Add the post-tool and exception-injection rows.
