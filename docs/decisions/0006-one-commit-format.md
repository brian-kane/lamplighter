# 0006: One commit format in every repo I work in

Status: Accepted

Date: 2026-10-16

## Decision

- Every commit uses the Conventional Commits form `type(scope): summary`, imperative, under 72 characters.
- Types are `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, `build`.
- Where history is mixed, it stays mixed.
- Commits created by the hosting platform (for example the initial commit) are exempt.

## Reason

- Conventional Commits is a published, widely used convention, so people and agents already know it.
- The type tells a reviewer the kind of change at a glance.
- The format is machine-readable, so a commit-message check and changelog tooling can rely on it. **Gap:** the commit-message check is planned, not built.
- One format everywhere is one habit instead of one per repo.

## Alternatives rejected

- Per-repo formats: each repo needs its own habit, and tooling can rely on none of them.
- Free-form subjects: tooling cannot read them.
- Rewriting old history to match: it rewrites published commits for a cosmetic gain.

## Revisit trigger

A repo needs a type outside this list.
