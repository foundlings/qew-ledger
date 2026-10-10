id: 042cxmtjh
kind: issue
title: Cover pre-tool refusal classes the reference exercises: write vs read, disable-auto, wrappers, prefixes, quotes
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
Pre-tool refuses forge bypasses structurally (tokenized, never executed) and stays silent for reads, quoted text, empty or unterminated input. Qew refuses instead of warns (a ledger-first design decision) so every expectation below is a deny with the qew command named.

## Scenarios
- Write matrix: issue create/edit/close/reopen/comment, `pr create` is NOT refused in qew (decision recorded), chained `git status && gh issue edit 3`, and env-prefixed absolute path `FOO=1 /opt/homebrew/bin/gh issue edit 3` are each denied and name the matching qew command (`qew set`, `qew create`, `qew complete`, `qew reopen`). Prevents a prefix or chain evading the guard.
- Merge forms `gh pr merge 3 --merge`, `--auto 3`, bare `gh pr merge` are denied pointing at `qew pr merge` or its ledger equivalent; `--disable-auto` is allowed and silent. Prevents auto-merge landing with pending checks, and over-blocking its cancellation.
- Reads and quoted text silent: `gh issue view|list`, `gh pr view`, `echo "gh issue edit 3"`, `ls -la`, unterminated `'quote`, empty command. Prevents a noisy guard that trains agents to ignore it.
- Outside a Qew-managed repository nothing is refused and no call is made.
- Advice matches the blocked action (covered).

## Reference coverage
6 pre-shell tests merged here (raw writes warn; raw merge pointed at pr merge; disable-auto silent; reads and quoted silent; outside repo silent; advice naming).

## Qew today
Largely covered by the hook v1 walk bypass, advice, reads/quoted, outside-repo scenarios. Missing: env-prefix plus absolute-path gh, chained commands, `--auto`/bare merge forms and the disable-auto allowance as explicit rows; confirm each.
