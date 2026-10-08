id: 042cxmtjb
kind: issue
title: Execute the generated opencode plugin under node against a fake qew and prove it never throws
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
The generated plugin pipes the bash tool's command to `qew hook pre-tool|post-tool --agent opencode` with a fixed executable and argv, and appends hook text to the tool output. A deny (exit 2, reason on stdout) throws to block the tool call; any other qew failure, a missing qew binary or non-bash tools must never throw.

## Scenarios
- node run, fake qew on PATH, three tool calls (bash ok, read, bash with qew failing exit 3): outputs and the recorded argv/stdin match; non-bash tool never invokes qew; qew failure leaves output untouched. Prevents the plugin crashing the agent or shelling out for unrelated tools.
- Deny path: fake qew exits 2 with a reason; the before hook throws that reason, the after hook does not run for the blocked call.
- Skipped cleanly when node is absent.

## Reference coverage
1 test (opencode plugin pipes bash commands and never throws).

## Qew today
Missing. Qew's opencode plugin is only checked as installed text; no walk executes it.
