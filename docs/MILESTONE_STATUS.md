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
- 0.8 — Service responsibility mapping;
- module boundary vs runtime/deployment boundary;
- ownership and coupling basics;
- failure propagation / blast-radius basics;
- why shared data access weakens service independence;
- why long synchronous dependency chains create request coupling;
- distributed-monolith warning signs;
- business-capability decomposition rather than table/technical-layer decomposition;
- bounded-context reasoning using responsibility, source of truth, business rules, cohesion, and reasons to change;
- distinction between Course, Payment, Enrollment, Auth/Profile, and Learning Progress ownership.

## Still Pending

Continue the established Milestone 0 lesson sequence exactly:

- Reinforcement block before 0.9 — cross-domain practice for discovering bounded contexts, defining responsibility, identifying source of truth, and mapping service boundaries. This is learner-requested reinforcement after completing 0.8 and must happen before starting 0.9;
- 0.9 — Data ownership and database-per-service;
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
- Auth/Profile, Enrollment/Learning Progress, and Course/Payment responsibilities can reference the same real-world user/course while owning different business truths;
- Course owns course configuration/publishing truth, Payment owns financial transaction/refund truth, and Enrollment owns access-entitlement truth.

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

Sections **0.1 through 0.8 are complete as curriculum sections**.

No implementation work has been performed, and Milestone 0 remains in progress.

The learner explicitly requested **additional reinforcement before 0.9** because they are not yet confident independently discovering bounded contexts, articulating the business question a context answers, identifying source-of-truth ownership, and mapping responsibilities/services without relying on memorized platform examples.

Resume with a **cross-domain reinforcement block** using unfamiliar domains. Do not start 0.9 automatically.

After the reinforcement block demonstrates stronger independent reasoning, explicitly ask the learner whether they want to start **0.9 — Data ownership and database-per-service**. If a new conversation begins before that decision, the mentor should resume reinforcement first and then ask whether to start 0.9.

## Next Engineering Step

No code/infrastructure action yet.

After the reinforcement block and sections 0.9–0.13 are completed, draft the **first system architecture diagram and service responsibility map** in sections 0.14–0.15. Do not start application coding before the Milestone 0 assignment has been evaluated.

## Session Update Rule

At the end of every substantial learning/building session, update this file with:

- the real current milestone and status;
- newly implemented work;
- remaining work;
- relevant files/components changed;
- verification performed;
- completion-gate state;
- one precise **Next Engineering Step**.

Preserve completed-milestone history, but do not turn this file into a session transcript.
