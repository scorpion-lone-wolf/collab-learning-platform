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

**Status:** NOT STARTED

## Completed Milestones

None.

## Implemented

No project implementation has been recorded yet.

## Still Pending

Milestone 0 must cover and produce the required architecture understanding/artifacts, including:

- monolith vs modular monolith vs microservices;
- why microservices are difficult and when they are not the right starting point;
- bounded contexts;
- service ownership and responsibility mapping;
- database-per-service and data ownership;
- synchronous vs asynchronous communication;
- first system architecture diagram;
- service responsibility map;
- first architecture decision records where an actual durable decision is made;
- Milestone 0 checkpoint;
- Milestone 0 assignment and grading;
- Milestone 0 completion-gate review.

## Relevant Files / Components

- `docs/MASTER_CURRICULUM.md` — curriculum, milestone order, architecture, and teaching rules.
- `docs/MILESTONE_STATUS.md` — engineering progress and next engineering step.
- `docs/LEARNING_STATE.md` — demonstrated understanding and next teaching step.
- `docs/DECISIONS.md` — durable architecture decisions and their history.

No application/service implementation files are active yet.

## Verification Already Performed

None. The project is still in the initial bootstrap state.

## Current Milestone Completion Gate

- [ ] Problem and motivation explained.
- [ ] Mental model / first system view explained.
- [ ] Tradeoffs discussed.
- [ ] High-level architecture responsibilities and boundaries defined.
- [ ] Required Milestone 0 artifacts produced.
- [ ] Important failure/operational implications discussed where relevant.
- [ ] Common mistakes and production best practices reviewed.
- [ ] Checkpoint completed.
- [ ] Assignment completed and graded.
- [ ] Architecture/documentation updated as required.

## Next Engineering Step

After the Milestone 0 problem/mental-model teaching, draft the **first system architecture diagram and service responsibility map**. Do not start application coding before the service boundaries and ownership model are understood and the Milestone 0 assignment has been evaluated.

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
