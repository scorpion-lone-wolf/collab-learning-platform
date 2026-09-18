# Learning State

> **Purpose:** Track what the learner has actually demonstrated they understand while building the Collaborative Learning Platform.
>
> **Hard rule:** Explanation does not equal understanding. Move a concept into **Understands** only after it is demonstrated through reasoning, implementation, debugging, prediction, explanation, a checkpoint, or an assignment.

## Curriculum Alignment

- Curriculum: `docs/MASTER_CURRICULUM.md`
- Current teaching position must stay aligned with `MILESTONE_STATUS.md`.
- Follow the Teaching Contract and the single **Authoritative Step-by-Step Milestone Sequence**.
- Do not skip ahead simply because a future topic is related to the current one; record nonessential future topics in the Parking Lot instead.

## Current Milestone

**Milestone 0 — Architecture Orientation and System HLD**

**Learning status:** IN PROGRESS

## Understands

- a monolith can contain multiple clean internal modules and still be one deployment/runtime unit;
- a modular monolith uses explicit internal ownership/boundaries without becoming multiple services;
- a microservice boundary is stronger than a module boundary because it introduces an independent runtime/deployment boundary;
- business data should be modified by the capability/module/service that owns it;
- Payment directly mutating Enrollment data is tight data-ownership coupling;
- a long required service call chain such as Auth -> Course -> Payment creates request/runtime coupling;
- tightly coupled failures can increase blast radius;
- a successful core business operation should not necessarily fail because a non-critical notification dependency fails.

## Partially Understands

- comparison/tradeoff reasoning across monolith, modular monolith, and microservices has been introduced but should be consolidated in section 0.5;
- microservice difficulty/failure modes have been introduced but should be consolidated in section 0.6;
- broader service-boundary selection criteria still need bounded-context exercises;
- sync-vs-async decisions have only been introduced conceptually.

## Needs Reinforcement

- bounded contexts;
- source-of-truth/data ownership across independently deployed services;
- choosing service boundaries from business capabilities rather than tables or technical layers;
- synchronous vs asynchronous communication tradeoffs.

## Misconceptions / Weak Areas

None currently recorded as unresolved.

## Resolved Misconceptions

- clarified that a monolith does not automatically mean one failure always breaks every capability;
- clarified that microservices do not automatically guarantee failure isolation.

## Completed Understanding Checks

- identified one NestJS application with multiple modules as a monolith;
- identified Enrollment as the owner of enrollment-state changes;
- explained why Payment directly changing Enrollment data creates tight coupling;
- identified shared-database coupling and request-chain coupling in a nominal microservice setup;
- chose to preserve enrollment success when notification delivery fails and justified the business reason.

## Assignment History

No milestone assignment has been submitted or graded yet.

## Current Assignment Status

No active assignment yet.

## Parking Lot

No deferred topics recorded yet.

## Session Checkpoint

The session ended immediately after section **0.4 — Microservices** and its understanding check.

The learner demonstrated the core distinction between independently deployed services and internal modules, and correctly identified both shared-data coupling and synchronous request-chain coupling.

## Next Teaching Step

Resume exactly at **0.5 — Monolith vs modular monolith vs microservices**.

Then continue in this order:

1. 0.5 — consolidate the three architecture styles and their tradeoffs;
2. 0.6 — formally cover why microservices are difficult;
3. 0.7 — Business capabilities and bounded contexts.

Do not restart sections 0.1–0.4. Do not skip or renumber the established Milestone 0 subsections.

## Session Update Rule

At the end of every substantial learning session, update this file with:

- newly demonstrated understanding;
- concepts that are only partially understood;
- weak areas or misconceptions;
- completed reasoning checks/assignments and their real verdicts;
- deferred topics worth preserving;
- one precise **Next Teaching Step**.

Keep this file concise enough that a new session can reconstruct the learner's actual position quickly.
