id: 042fnqv0x
kind: issue
title: Cross-repository references kept as untrusted text links
parent: 042fnqu4s
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T01:42:09Z
---
References like owner/repo#123 in imported text are recorded as links on the item (display only, never followed, never turned into edges) and shown by qew show; qew check validates the syntax only.
