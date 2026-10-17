# 0001: Rebase-only merges

Status: Accepted

Date: 2026-10-16

## Decision

Pull requests merge by rebase only; the protect-main ruleset enforces it.

## Reason

- Commits here are curated on purpose: the agent may rewrite its own branch, changes are grouped by blast radius, and each commit body carries the why (see [0007](0007-one-documentation-standard.md)).
- Rebase keeps every commit with its own message on main and keeps history linear, so `git log`, `git blame` and `git bisect` work commit by commit.

Costs, stated plainly:

- Rebasing rewrites commit hashes, so a merged local branch looks unmerged and must be deleted with `git branch -D`.
- Every commit must stand on its own, and only a CI job that checks every commit can prove that. **Gap:** that CI job is planned, not built.

## Alternatives rejected

- Squash merges: one commit per PR discards the curated commits and makes the squash message, which is set at merge time rather than curated on the branch, the permanent record. That reverses [0007](0007-one-documentation-standard.md).
- Merge commits: they keep the commits but add merge commits and a branching history, which buys little with one contributor and short-lived branches.

## Revisit trigger

A second contributor joins, or curating commits costs more than the per-commit history is worth.
