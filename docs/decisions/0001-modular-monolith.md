# ADR 0001: Start with a Modular Monolith

Status: Proposed

Date: 2026-07-16

## Context

The platform must replace Moodle, support a mobile-first learner experience and an admin portal, migrate complex content, retain learning history, and scale from a few thousand users toward 10,000 with examination peaks.

The main early risks are content migration, scoring fidelity, product access rules, security, and user experience. They are not independent-service throughput or organization-scale deployment ownership.

## Decision

Build the learner UI, admin UI, versioned API, and domain modules in one deployable application backed by PostgreSQL. Run long-lived web traffic and background work as separate process types from the same codebase and container image.

Keep explicit module boundaries for identity, access, content, learning, admin, import, operations, and future AI integration. Enforce boundaries through code ownership and public module APIs rather than network calls.

## Consequences

Positive:

- one codebase, deployment pipeline, and transactional data model;
- simpler development, testing, incident response, and local setup;
- atomic access redemption, answer submission, and publishing workflows;
- enough horizontal scaling for the expected user population;
- modules can be extracted later without designing speculative services now.

Trade-offs:

- a defect or deployment can affect multiple modules;
- module boundaries require discipline because the database is shared;
- web and worker processes share a release cadence initially.

## Revisit when

Extract a module only when at least one measurable condition exists:

- it requires materially different scaling or availability;
- a separate team owns and releases it independently;
- its security or data-residency boundary cannot be enforced in the application;
- background workload harms learner-request latency despite process isolation;
- measured database or deployment coupling becomes a material constraint.

Until then, Kubernetes, Kafka, a service mesh, and per-module databases are out of scope.
