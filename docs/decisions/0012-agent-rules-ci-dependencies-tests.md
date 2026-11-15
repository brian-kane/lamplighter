# 0012: Agents may change CI when asked, add no dependency unasked, and test behavior changes

Status: Accepted

Date: 2026-11-15

## Decision

- The shared agent rules keep "ask before changing CI, hooks, rulesets, or credential configuration", except where the issue or prompt's task is to change them.
- An agent adds no dependency without asking first, and says what it replaces and why building it isn't better.
- A behavior change comes with a test that fails without it.
- The rules are in [agents/shared-rules.md](../../agents/shared-rules.md) under Boundaries and Checks.

## Reason

- A task whose whole purpose is to change CI or hooks was blocked by an ask-first rule the owner had already answered by assigning the task.
- A new dependency is a standing cost the owner should choose, so the agent asks and states what it replaces.
- A test that passes with and without a behavior change proves nothing about the change.

Gap: nothing enforces these rules. The dependency rule and the test rule are conventions the owner checks in review ([0009](0009-reviewer-is-advisory.md) makes automated review advisory).

## Alternatives rejected

- Keep the CI and hooks rule absolute: tasks that exist to change CI or hooks would need a second confirmation.
- Let agents add dependencies and report them afterwards: the owner would review a cost already paid.
- Ask for tests only on bug fixes: a behavior change that is not a fix would go unproven.

## Revisit trigger

- A dependency or a behavior change merges without the ask or the failing test.
- A deterministic check can detect an added dependency or a change without a test; then enforce the rule with that check, proven by a planted failure ([protocol rule 4](../SESSION-PROTOCOL.md#4-automate-what-has-been-done-by-hand-and-written-down)).
