id: 042fit8cu
kind: issue
title: qew item rename: move an item to another id, keeping the old one as an alias
parent: 042ffd5dc
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T00:21:53Z
evidence: wpmxrrwquurx sulmzpsynxqn
---
Owner 2026-10-10: 'yes please move stuff' (PIE, a hand-named epic in foundlings, to the next letter, ADG). qew item rename ITEM [NEW]: NEW defaults to the next free id of the item's kind; a letters kind accepts only the next letter. Reuses the migrate-ids machinery (item file, events, mirrors, attachments directory, links, views, local state; old id stays an alias; forge markers are adopted and rewritten on the next sync); refuses while another login holds a claim; one ledger commit; --dry-run. Then rename foundlings' PIE.
