# 0010: Agents push branches and open pull requests in personal repos

Status: Accepted; the push credential is changed by [0011](0011-agent-token-may-push.md) for repos with no deploy key

Date: 2026-11-14

## Decision

- In a personal repo whose CLAUDE.md allows it, the local agent pushes its own branch over the repo's deploy key and opens a draft pull request with `gh`. It never pushes `main` and never merges; the owner merges by rebase ([0001](0001-rebase-only-merges.md)).
- `gh` in the personal distro uses a fine-grained token limited to that one repository: pull requests and issues read and write, contents and metadata read, no workflows, no administration. It expires within 90 days.
- Where no ruleset can protect `main` (a private repo on the free plan), a versioned `pre-push` hook refuses pushes to `main`. **Gap:** that hook guards only clones with hooks installed, and `--no-verify` skips it.
- This replaces, for those repos only, two points of [0003](0003-credentials-and-identities.md): that the owner pushes every change, and that no GitHub account credential is stored in the personal distro.

## Reason

- Pushing by hand and pasting agent reports into the planning chat were the main manual steps. With the branch and draft PR on GitHub, the planning chat reads them through the Claude GitHub App, and the owner reviews and merges from any device.
- The token is narrow, short-lived and revocable, and it has no administration access, so nothing it reaches can weaken a ruleset ([0004](0004-developer-experience-over-security.md)'s exception holds).
- A local agent could already push while the deploy keys were loaded (the tradeoff stated in 0003), so the new reach is limited to pull requests and issues on one repo.

Cost, stated plainly: the token is stored where the local agent can read it.

## Alternatives rejected

- The owner keeps pushing and pastes reports into the chat: the manual steps stay.
- Cloud sessions only, acting through the App: too few cores for the sim's screens.
- A classic personal access token, or a bot account ([0003](0003-credentials-and-identities.md)).
- Paying for a plan that protects `main` on private repos.

## Revisit trigger

- A token is used outside its repository or permissions.
- A ruleset can protect `main` on the repo, or the planned dev container exists (then the token moves into it).
- A second contributor joins.
