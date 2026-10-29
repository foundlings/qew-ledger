id: 042cxmtju
kind: issue
title: Check `qew release` (give up a claim) against the reference claim-release guarantees
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: pmytyxoosnrz
---
## Behaviour
Overlaps the lifecycle area; listed here because the reference test file name contains release. Releasing a claim frees the item for others and records who, which lane and why in the ledger event; ledger-first means no forge labels or comments.

## Scenarios
- Golden: release records actor, lane and reason; item returns to ready; text and `--json` output (state released, lane, by).
- Unclaimed item refused without writing; closed item refused without writing.
- Another actor's claim refused with a message naming the holder and `--force`; forced release records the releaser.
- A lane-scoped claim cannot be released without naming that lane; forcing from another lane records that in the event. Prevents sibling lanes freeing live work.
- Empty or whitespace reason refused before any write.
- A reason cannot forge or terminate another record (no marker injection in event text; JSON-escaped).
- Malformed claim record in the ledger does not block release but warns on stderr (qew: `qew check` reports instead).
- Post-write verification: item still claimed afterwards fails loudly (exit 3).
- Stale claim state with no holder is releasable.

## Reference coverage
13 tests in the reference release walk file, merged into the scenarios above.

## Qew today
`qew release` exists; only a single golden call in the flow walk. Everything else needs scenarios (coordinate with the lifecycle audit so work is not filed twice).
