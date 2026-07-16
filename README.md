# Scariev Learning Platform

Architecture and delivery workspace for replacing the existing Moodle-based medical exam preparation platform.

## Current status

The project is in architecture discovery. No production application has been scaffolded yet. The first deliverable is a concise 1–3 slide architecture proposal and initial implementation plan.

## First deliverable

The proposal covers:

- target architecture and technology recommendation;
- core data model;
- Moodle import for questions, formulas, and images;
- learner and admin capabilities;
- identity, time-limited access, and print-code redemption;
- security, privacy, monitoring, and scaling;
- implementation phases and major open decisions.

## Architecture snapshot

The current recommendation is a modular monolith:

- Next.js, React, and TypeScript for the mobile-first learner experience and admin portal;
- a versioned HTTP API in the same deployable application;
- managed OIDC authentication with an internal UUID-based user model;
- PostgreSQL as the system of record;
- object storage and CDN for images and source imports;
- a background worker from the same codebase for imports and other long-running jobs;
- an AWS reference deployment using CloudFront/WAF, ECS Fargate, RDS PostgreSQL, S3, SQS, and CloudWatch;
- future AI functions behind a controlled gateway and the existing access-grant model.

See [Target Architecture](docs/architecture.md), [Implementation Plan](docs/implementation-plan.md), and [ADR 0001](docs/decisions/0001-modular-monolith.md).

## Planned application structure

Application directories will be added after the architecture spike confirms the Moodle format, hosting constraints, and framework choice.

```text
apps/
  platform/             learner and admin web application plus API
packages/
  database/             schema, migrations, and database access
  moodle-import/        parser, normalizer, validation, and import reporting
infrastructure/         deployment and infrastructure as code
docs/                   architecture, decisions, and delivery plan
```

## Decisions still needed

1. Whether AWS in an EU region is acceptable.
2. Whether the migration includes Moodle users, access periods, and progress or only content.
3. A representative Moodle export and inventory of question types/plugins.
4. Whether product access starts at purchase, code redemption, or first use.
5. Whether products unlock a fixed exam edition or always-current content.
6. The expected peak number of concurrent learners.
