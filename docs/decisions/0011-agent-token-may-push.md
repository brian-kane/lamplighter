# 0011: The agent's token may push where a repo has no deploy key

Status: Accepted

Date: 2026-11-14

## Decision

- In a personal repo that has no deploy key on the machine, the fine-grained token from [0010](0010-agents-open-pull-requests.md) also has contents read and write, and git pushes over HTTPS through `gh`'s credential helper.
- Everything else in 0010 stands: one repository per token, no workflows, no administration, 90-day expiry, the agent never pushes `main` or merges, and the `pre-push` hook refuses `main` where no ruleset can.

## Reason

- seekers has no deploy key on the personal distro; its pushes always went through `gh`'s login, and signing `gh` in with the 0010 token (contents read-only) made every push fail with 403, the owner's included.
- Adding a deploy key per repo is a manual step per repo; one token per repo that both opens PRs and pushes keeps it to one credential.

Cost, stated plainly: the token can now push any branch of its repo, including `main` if the hook is skipped (`--no-verify`). On a free private repo nothing on GitHub stops that.

## Alternatives rejected

- Add a seekers deploy key and push over SSH: a second credential for the same repo, and pushes fail whenever the keychain has timed out.
- A classic token with broad scope ([0003](0003-credentials-and-identities.md)).

## Revisit trigger

- A push to `main` happens outside a merge.
- A ruleset becomes available on the repo, or the planned dev container exists.
