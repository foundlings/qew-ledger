id: 042cxmtm6
kind: issue
title: Derive the PR body sections from the item and refuse closing references in any body text
parent: 042cxmtm4
needs: 042cxmtm5
labels: area:pull-requests
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
The PR body is built from the item body (What / Why / Testing sections, optional `--what/--why/--testing/--body-file` overrides) plus the marker and the `Delivers ID` line. Item and caller text is untrusted: ANY closing keyword (`closes|fixes|resolves`, any case, with `#N`, `owner/repo#N` or an issue URL, in-line or at line start, `closed:` forms) anywhere in the final body is refused (exit 2) before the forge is called, because the ledger, not a forge side effect, completes work (see ledger.md: pull requests never carry a closing keyword). A `Part of`/`Delivers` back-reference is allowed.

## Scenarios
- golden body: item with goal/approach sections -> PR body contains the sections once, the marker once, `Delivers ID` once. Prevents: lost or duplicated provenance.
- closing keyword adversary table: in-line `also fixes #16`, `Resolves acme/other#7`, `closed: #16`, `Closes https://host/o/r/issues/9`, `fixes o/r#16` in an item body or `--what` text are each refused with exit 2 and no forge call. Prevents: merging the PR closing unrelated issues on the forge behind qew's back.
- no rewrite: text that merely mentions a flag or path is passed through byte for byte. Prevents: silent body mutation.

## Reference coverage
Reference pull-request lifecycle walk file: golden derives title/body, closing-reference refusal table (5 cases, one test function).

## Qew today
Reduced: `open_pull_request` writes a fixed body (marker + `Delivers`) and never reads item body text, so there is no section derivation and no scanner for caller-supplied text. The scanner must exist before any `--body-file`/`--what` option or item-body copy is added.
