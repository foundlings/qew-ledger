id: 042cxmtk9
kind: issue
title: Allow completion without a code change only with an explicit recorded reason
parent: 042cxmtjw
needs: 042cxmtk2
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
A task whose delivery is not in the repository (docs elsewhere, a decision) cannot be completed in qew today except through import. `qew complete ITEM --reason TEXT --no-commit WHY` records `no_commit: WHY` on the `completed` event and skips the landing proof; exactly one of evidence-on-target or `--no-commit` must hold, and a blank `WHY` is refused. `qew check` counts these like imports: `completed without code: N` (non-fatal). A reason alone never proves anything landed.

## Scenarios
- golden: claimed item, `--no-commit` with a reason; completes, event records it (prevents: forcing fake evidence for non-code work)
- no evidence and no `--no-commit`: refused (covered by test_complete_is_refused_without_evidence)
- both evidence and `--no-commit`, blank `WHY`: exit 2, zero events (prevents: contradictory flags silently picking one meaning)
- check lists such items so reviewers can audit them (prevents: `--no-commit` becoming the default escape hatch)

## Reference coverage
1 reference test function(s): `test_complete_requires_a_landed_commit_or_an_explicit_no_commit`

## Qew today
Missing. Evidence-less completion is refused (covered), but the explicit alternative does not exist.
