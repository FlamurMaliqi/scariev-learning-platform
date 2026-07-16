# Initial Implementation Plan

Status: Draft

Last updated: 2026-07-16

The phases describe scope and dependencies. Calendar estimates should be added only after team size, content complexity, external integrations, and migration scope are known.

## Phase 0: Discovery and risk reduction

- Inventory Moodle versions, question types, plugins, users, access periods, and progress data.
- Obtain a representative export containing the most complex formulas, images, and grading rules.
- Build a narrow parser/rendering spike and compare results with Moodle.
- Confirm cloud, identity, payment, privacy, availability, and retention constraints.
- Agree peak concurrency and load-test targets.
- Finalize the architecture decision and MVP acceptance criteria.

Exit criterion: supported and unsupported migration cases are known, and no unresolved constraint invalidates the target architecture.

## Phase 1: Platform foundation

- Establish repository tooling, continuous integration, environments, and infrastructure as code.
- Deploy a minimal platform with health checks, structured logging, metrics, and secrets management.
- Integrate managed OIDC authentication and create internal UUID users.
- Implement access scopes and grants.
- Add the first admin security boundary, roles, MFA policy, and audit events.

Exit criterion: a learner and administrator can authenticate in a non-production environment, and protected access is enforced server-side.

## Phase 2: Learning and access MVP

- Implement courses/topics, versioned questions, server-side grading, sessions, deliveries, attempts, and progress.
- Build the mobile-first learning flow and basic accessibility behavior.
- Implement print-code batches and atomic redemption.
- Add online-purchase webhook integration if it is in MVP scope.
- Deliver admin user search, access inspection, grant, extension, and revocation.

Exit criterion: an entitled learner can complete a representative learning session and an administrator can support the account safely.

## Phase 3: Content administration and Moodle migration

- Complete the supported Moodle parser and deterministic normalizer.
- Extract, validate, and store images and formula sources.
- Add import runs, diagnostics, idempotency, conflict detection, and replay.
- Deliver admin import preview, question revision history, editing, approval, and publishing.
- Run migration rehearsals and reconcile counts, renders, and scoring outcomes.

Exit criterion: approved content can be migrated repeatedly without duplication or silent scoring changes.

## Phase 4: Production readiness and cutover

- Run security, accessibility, performance, and failure-recovery tests.
- Load-test the agreed examination peak and configure scheduled/autoscaling capacity.
- Validate backups through restoration and test monitoring/incident response.
- Complete privacy workflows for export, deletion, and retention.
- Pilot with selected users, resolve migration discrepancies, and rehearse rollback.
- Freeze Moodle content, run the final migration, reconcile, and cut over.

Exit criterion: operational, migration, and product owners approve go-live and rollback readiness.

## Later increments

- AI tutor grounded in approved content.
- Paid AI feature grants, usage limits, and separate conversation retention.
- Rule-based adaptive learning followed by measured model experiments.
- Data warehouse, additional services, or native apps only when product or operational evidence justifies them.

## First slide deliverable

Recommended three-slide structure:

1. Target architecture, technology choices, and modular-monolith decision.
2. Data model, Moodle import, admin scope, security, and scaling.
3. Implementation phases, key risks, open decisions, and immediate next steps.
