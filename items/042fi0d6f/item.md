id: 042fi0d6f
kind: issue
title: A clean sync leaves pending=N: events that change nothing on the forge never advance synced_event
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T00:05:38Z
---
Santa 2026-10-10 (foundlings, 1871 mirrors): qew status kept pending=2 after a sync that reported unchanged 1871. The two were WP-AAV-06 (newest event divergence_accepted) and 042ezifgw (newest event commented): the fingerprint was unchanged so the sync skipped them, but never recorded the newest event as synced, and pending is derived from synced_event != newest event. Fix: in the unchanged branch record synced_event.
