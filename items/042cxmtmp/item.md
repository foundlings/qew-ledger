id: 042cxmtmp
kind: issue
title: Pin forge-launch failure behaviour: unreachable, hung and tokenless forges give one line, no traceback
parent: 042cxmtm4
needs: 
labels: area:pull-requests
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
Every forge call has a bounded timeout (default 30 s, the `urllib_transport` timeout; configurable through the `timeout` mirror option, YAGNI otherwise) and failures are typed: unreachable or timed out -> `ForgeUnavailable`, missing token -> `ForgeAuth` before any request. The pr commands (`open`, `ready`, `merge`) print one stderr line with the target and the cause and exit 1, never a Python traceback. The mirror-slug lookup for a recorded pr whose mirror left the config is a typed refusal, not `StopIteration`. A token resolved from `gh auth token` fails closed when the helper hangs or is missing (falls to ForgeAuth).

## Scenarios
- hung forge: a server that never answers -> exit 1 within the timeout, line says timed out, no traceback, no mirror file. Prevents: a hook or agent hanging forever.
- no token: exit 1 naming the environment variables, zero requests. Prevents: anonymous requests or leaked guessing.
- pr mirror points at a target no longer configured: exit 2 'target X is not configured', no traceback. Prevents: StopIteration crash.
- missing/hung `gh auth token` helper falls back to ForgeAuth. Prevents: hang in token resolution.

## Reference coverage
Reference gh launch walk file: missing gh exits three without traceback, hung gh times out with exit three. 2 test functions; the missing-binary half is dropped (qew does not launch gh for requests).

## Qew today
Covered in part: backend walks assert unreachable host -> ForgeUnavailable and missing token -> ForgeAuth for GitHub, Forgejo and GitLab. Missing: the command-level exit/line/no-traceback walk through `qew pr`, a hung-server walk, the unconfigured-target refusal; `cmd_pr._mirror_for` uses a bare `next()`.
