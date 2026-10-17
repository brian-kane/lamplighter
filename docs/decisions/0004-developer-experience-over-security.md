# 0004: Developer experience over security when they conflict

Status: Accepted

Date: 2026-10-16

## Decision

When developer experience and security conflict, developer experience wins, except that nothing the agent can reach may weaken the ruleset.

## Reason

The safe path must also be the easy path, or steps get skipped. The ruleset is the one control the agent must never be able to loosen.

## Alternatives rejected

- Security-first by default.

## Revisit trigger

Any convenience is found that lets something the agent can reach weaken the ruleset, or a second contributor joins.
