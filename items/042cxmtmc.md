id: 042cxmtmc
kind: issue
title: Add `qew pr check NUMBER (ID... | --all | --list)` to tick PR progress items in place
parent: 042cxmtm4
needs: 042cxmtm7 042cxmtmb
labels: area:pull-requests
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
Ticks `- [ ]` lines of a recorded PR's body outside code fences, addressed by `<!-- pr-progress:ID -->` marker, else by 1-based position (`@N` when a marker already uses N). Unknown ids and duplicate ids are exit 2 before any write. The body is re-read immediately before the write and the write is skipped (exit 3) if the body changed since the first read (no compare-and-set exists on forges; the residual window is documented); the result is read back and verified, and a write that did not stick is exit 3. The rest of the body, including line endings, is preserved byte for byte. An already-ticked item writes nothing. `--list` prints each item and whether it is ticked, writes nothing. The command is listed in the `--help` epilog group, README and commands.md.

## Scenarios
- golden: marked items -> tick one, forge body differs only by that box, verified by read-back. Prevents: a rebuilt body that drops trailers or text.
- position addressing and `@N` fallback when a marker id equals a position (marker '2' on item 1 and markerless item 2): both addressable, body readable. Prevents: ambiguous or unreadable bodies.
- `--all` ticks every open item; already ticked item writes nothing (changed list empty, zero edits). Prevents: spurious edits.
- unknown item and duplicate item ids: exit 2, zero writes. Prevents: partial ticking.
- code fences: items inside ``` or ~~~ blocks do not count; one-line fences and shorter closing fences follow CommonMark. Prevents: a hidden open box letting `qew pr merge` pass.
- CRLF body ticked without changing line endings. Prevents: whole-body diffs.
- concurrent human edit between read and write: refused exit 3, zero writes. Prevents: losing a teammate's edit.
- write that did not stick (forge returns old body): exit 3. Prevents: reporting success for a failed write.
- `--list` shows items and ticked state without writing; a body without a checklist says so.
- naming items together with `--all` or `--list` or neither is exit 2 before any forge call. Prevents: ambiguous intent.
- merged or closed PR refused exit 2 with zero writes. Prevents: editing history.
- ownership refusals are covered by pr-owner-rule.

## Reference coverage
Reference pr check walk file: 19 test functions (tick marked, position, all, already ticked, unknown item, code block, fence rules, CRLF, marker equals position, duplicate id, edited meanwhile, teammate holds claims, teammate missing claim, other login, merged PR, write not sticking, list, no checklist, mutually exclusive options). Ownership ones (3) go to pr-owner-rule.

## Qew today
Missing entirely: no `pr check` subcommand, no checklist model, `RemotePullRequest` carries no body.
