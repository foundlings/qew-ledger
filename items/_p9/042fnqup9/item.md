id: 042fnqup9
kind: issue
title: Issue body edit history imported at import time
parent: 042fnqu4s
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T01:42:09Z
evidence: ylyppumrnxkn uzuowlorwwxs
---
On import, read the body edit history (GraphQL userContentEdits) and record body_revision events (editor, time, text hash and text up to a limit, provenance forge-import); the current body stays the item body. Not mirrored back.
