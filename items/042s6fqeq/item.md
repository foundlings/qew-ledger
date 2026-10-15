id: 042s6fqeq
kind: task
title: start --take-over refuses a claimed item whose needs are open: a handoff re-checks readiness
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-15T19:04:35Z
---
cmd_claim.start runs the blockers check on a take-over too, so an owner-authorized handoff of claimed work whose needs are open (or each other) is refused and the new holder cannot take the claim. Blockers gate starting work, not changing hands: a take-over of a claimed item moves the claim, records the reason and leaves the needs alone. Reported by foundlings (elf5 to elf2, seven stacked provider tasks under 4466 needing 042pcoy9h).
