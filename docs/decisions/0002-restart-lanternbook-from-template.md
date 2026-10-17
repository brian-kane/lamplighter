# 0002: Restart Lanternbook from a Lamplighter template

Status: Accepted

Date: 2026-10-16

## Decision

Lanternbook stays paused and is restarted from a Lamplighter template, not evolved from its current state.

## Reason

Earlier repos built automation before the product and let checks and docs drift; a tested template carries the process in tooling.

## Alternatives rejected

- Retrofitting the existing Lanternbook repo.
- Continuing Lanternbook now without the template.

## Revisit trigger

The template can create a repo that passes its required check on the first PR; at that point the restart happens.
