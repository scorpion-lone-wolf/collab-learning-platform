# Milestone Status

> **Purpose:** Track the actual engineering state of the Collaborative Learning Platform.
>
> **Source-of-truth rule:** The current repository is authoritative for what code/infrastructure actually exists. `MASTER_CURRICULUM.md` is authoritative for milestone order and required scope. If this file disagrees with the repository, inspect the repository and correct this file.

## Curriculum Alignment

- Curriculum: `docs/MASTER_CURRICULUM.md`
- Progression source: **Authoritative Step-by-Step Milestone Sequence** in `MASTER_CURRICULUM.md`
- Do not use any alternate or historical milestone sequence.
- A milestone is complete only after its applicable definition-of-done items, checkpoint, assignment, and grading gate are satisfied.

## Current Milestone

**Milestone 0 — Architecture Orientation and System HLD**

**Status:** IN PROGRESS

## Completed Milestones

None.

## Implemented

No application/service implementation has started yet.

## Learning / Architecture Work Completed So Far

- 0.1 — Engineering problem / architecture pressures;
- 0.2 — Monolith;
- 0.3 — Modular monolith;
- 0.4 — Microservices;
- 0.5 — Monolith vs modular monolith vs microservices;
- 0.6 — Why microservices are difficult;
- 0.7 — Business capabilities and bounded contexts;
- 0.8 — Service responsibility mapping;
- 0.9 — Data ownership and database-per-service;
- module boundary vs runtime/deployment boundary;
- ownership and coupling basics;
- failure propagation / blast-radius basics;
- shared data access weakens service independence;
- long synchronous dependency chains create request coupling;
- distributed-monolith warning signs;
- business-capability decomposition;
- bounded-context reasoning using responsibility, source of truth, business rules, cohesion, and reasons to change;
- Course, Payment, Enrollment, Auth/Profile, and Learning Progress ownership distinctions;
- database-per-service as a logical ownership/access boundary, not necessarily one physical database server per service;
- direct cross-service database access creates schema and ownership coupling.

## Still Pending

Continue the established Milestone 0 lesson sequence exactly:

- 0.10 — Service contracts;
- 0.11 — Synchronous communication;
- 0.12 — Asynchronous communication;
- 0.13 — Sync vs async decision-making;
- 0.14 — First Collaborative Learning Platform HLD;
- 0.15 — Service responsibility map;
- 0.16 — First Architecture Decision Records;
- 0.17 — Failure and operational thinking;
- 0.18 — Architecture review;
- 0.19 — Checkpoint;
- 0.20 — Mandatory Milestone 0 assignment;
- 0.21 — Milestone 0 completion gate.

Additional bounded-context/responsibility-mapping reinforcement remains useful but is not a prerequisite for progression.

## Relevant Files / Components

- `docs/MASTER_CURRICULUM.md`
- `docs/MILESTONE_STATUS.md`
- `docs/LEARNING_STATE.md`
- `docs/DECISIONS.md`

No application/service implementation files are active yet.

## Verification Already Performed

Learner correctly reasoned that:

- one deployable NestJS application with multiple modules is still one monolith;
- Enrollment should own enrollment-state changes rather than Payment mutating Enrollment data directly;
- shared database access creates data-ownership coupling;
- a required Auth -> Course -> Payment request chain creates request/runtime coupling;
- a non-critical notification failure should not automatically invalidate a successful enrollment;
- a timeout does not prove that a remote payment failed;
- blindly retrying an ambiguous payment outcome can duplicate a charge;
- Course Management and Payment are separate bounded contexts even when they participate in one purchase workflow;
- Course owns current course pricing/configuration truth, Payment owns the historical amount actually charged, and Enrollment owns current course-access entitlement;
- Payment should not directly query Enrollment's database for access state because doing so violates ownership and couples Payment to Enrollment's internal schema;
- an Enrollment schema/field change should remain an Enrollment implementation detail rather than forcing Payment changes through direct database coupling.

## Current Milestone Completion Gate

- [x] Problem and motivation introduced.
- [x] Initial monolith / modular-monolith / microservice mental models explained.
- [x] Initial tradeoffs discussed.
- [ ] High-level architecture responsibilities and boundaries fully defined.
- [ ] Required Milestone 0 artifacts produced.
- [ ] Important failure/operational implications fully reviewed.
- [ ] Common mistakes and production best practices fully reviewed.
- [ ] Checkpoint completed.
- [ ] Assignment completed and graded.
- [ ] Architecture/documentation updated as required.

## Current Checkpoint

Sections **0.1 through 0.9 are complete as curriculum sections**.

The 0.9 understanding check was completed successfully: the learner separated current Course price, historical Payment charge amount, and Enrollment access state into their authoritative owners, and explained why direct cross-service database access creates ownership and schema coupling.

No implementation work has been performed, and Milestone 0 remains in progress.

## Next Engineering Step

No code/infrastructure action yet.

After sections 0.10–0.13 are completed, draft the **first system architecture diagram and service responsibility map** in sections 0.14–0.15. Do not start application coding before the Milestone 0 assignment has been evaluated.

## Session Update Rule

At the end of every substantial learning/building session, update this file with the real current milestone/status, newly implemented work, remaining work, relevant files/components, verification performed, completion-gate state, and one precise **Next Engineering Step**.
