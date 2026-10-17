# 0005: Network inspection

Status: Accepted

Date: 2026-10-16

## Decision

Where the network performs TLS inspection, install the inspection root CA in the system trust store. Never disable certificate verification, and never commit the certificate.

## Reason

Disabling verification removes the protection for every connection; the system store keeps tools working normally.

## Alternatives rejected

- Disabling verification globally or per tool.
- Committing the certificate.

## Revisit trigger

The network setup changes, or a tool with its own trust store needs separate handling (for example Node, where `NODE_OPTIONS=--use-system-ca` is unverified for the version in use).
