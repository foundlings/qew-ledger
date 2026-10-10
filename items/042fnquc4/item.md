id: 042fnquc4
kind: issue
title: PR reviews imported as comments on the covered item
parent: 042fnqu4s
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T01:42:09Z
---
For each open or merged pull request the item is tracked by, pull the reviews and review comments (REST pulls/N/reviews and pulls/N/comments) and import them as commented events on the first covered item with provenance forge, a remote_ref per review or review comment, the review state (approved, changes requested, commented) in the text header, and file/line for inline comments. Idempotent by remote_ref; only open PRs and PRs merged since the last pull are re-read; pacing and read limits as for issues.
