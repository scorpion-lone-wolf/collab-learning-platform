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

- engineering pressures that drive architecture decisions;
- monolith fundamentals;
- modular monolith fundamentals;
- microservice fundamentals;
- module boundary vs runtime/deployment boundary;
- ownership and coupling basics;
- failure propagation / blast-radius basics;
- why shared data access weakens service independence;
- why long synchronous dependency chains create request coupling;
- distributed-monolith warning signs.

## Still Pending

Milestone 0 still needs:

- bounded contexts;
- business-capability boundary reasoning;
- service responsibility mapping for the Collaborative Learning Platform;
- database-per-service and data ownership in more depth;
- synchronous vs asynchronous communication;
- first system architecture diagram;
- service responsibility map;
- first ADRs where a durable decision is actually made;
- Milestone 0 checkpoint;
- Milestone 0 assignment and grading;
- Milestone 0 completion-gate review.

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
- a non-critical notification failure should not automatically invalidate a successful enrollment.

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

## Next Engineering Step

After bounded contexts, service/data ownership, and sync-vs-async communication are taught, draft the **first system architecture diagram and service responsibility map**. Do not start application coding before the Milestone 0 assignment has been evaluated.

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
