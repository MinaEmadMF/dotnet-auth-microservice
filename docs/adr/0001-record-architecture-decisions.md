# 1. Record architecture decisions

## Status

Accepted

## Context

We need to record the architectural decisions made on the Auth Microservice
so that future maintainers understand why the system looks the way it does.

## Decision

We will use Architecture Decision Records (ADRs), stored in `docs/adr/` and
numbered sequentially (`0002-<short-title>.md`, ...). Each ADR has the
sections Status, Context, Decision and Consequences, and is added to the `nav`
in `mkdocs.yml`.

## Consequences

Significant decisions are reviewed in pull requests and published in
Backstage TechDocs alongside the rest of the service documentation.
