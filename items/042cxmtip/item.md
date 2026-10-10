id: 042cxmtip
kind: issue
title: Decide and build `qew plan create` for an epic with attached children
parent: 042cxmti7
needs: 042cxmtii
labels: area:drafts-plans
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
Reference `plan create --title ... --children 12,13 [--draft]` files an epic and attaches existing items as
children, reporting the created epic and the attached children if an attach fails (so a retry never creates a
second plan). Ledger decision to make first (YAGNI): `create --kind epic` followed by a multi-item
`set ITEM... --parent EPIC` may already be enough; if so close this issue and record it. If built:
- children are positive ids/aliases, unique, existing and valid under nesting; the epic cannot be its own child;
  non-ASCII digits are a usage error, not a traceback;
- `--draft` takes no `--children` (file them with `create --draft --parent`);
- the quote handling is that of `create`; attachment is validated for all children before the first write;
- a failure midway prints `created plan ID; attached: ...; not attached: ...; do not rerun plan create`.

## Scenarios
1. Golden: epic plus two children, JSON lists number and children, children now have `parent`. Prevents hand-wiring each child.
2. Failure on the second attach: stderr names the plan, attached and not attached ids, exit non-zero. Prevents a retry duplicating the plan.
3. Non-ASCII digit, zero, duplicate, self and unknown child ids exit 2 with no file written. Prevents a traceback or a half-built plan.
4. `--draft` with `--children` refused. Prevents filing a draft plan with live-looking attachments.

## Reference coverage
Reference graph-write: plan create golden walk creates approved parent and verifies children, plan create reports plan
and attached children on failure, plan create refuses non-ASCII digit children with usage error (3 of 26); requester
quote: plan create requires and renders the quote (1 of 9).

## Qew today
Missing: no plan commands; epics are created with `create --kind epic` and children attach with one `set --parent` each.
