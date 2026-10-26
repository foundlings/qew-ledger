id: 043ctryck
kind: issue
title: Name the repository, listing and cause when a listing is refused as too long
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-26T00:51:58Z
discovered_from: 0438zp3dj
---
## Problem

A page-cap refusal says only 'more than 50 pages; refusing a truncated listing': an agent cannot tell which repository or listing overflowed, or why the since-window did not apply, so it retries or guesses.

## Done when

ListingTooLong from pages() and from find_issue's no-window case names the repository path, the listing, the cap, and says whether the item id carried no mint time; a walk asserts each message.
