# 0009: The reviewer is advisory

Status: Accepted

Date: 2026-10-16

## Decision

Automated review comments never block a merge. When the same severe finding recurs, it becomes a deterministic check.

## Reason

An advisory reviewer cannot be trusted to gate, while deterministic checks can be proven with planted failures.

## Alternatives rejected

- A blocking reviewer.
- Ignoring recurring findings.

## Revisit trigger

When a deterministic check covers a recurring finding, retire the reliance on the reviewer for that finding.
