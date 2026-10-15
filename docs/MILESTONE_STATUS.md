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
- 0.10 — Service contracts;
- 0.11 — Synchronous communication;
- 0.12 — Asynchronous communication;
- 0.13 — Sync vs async decision-making;
- 0.14 — First Collaborative Learning Platform HLD is IN PROGRESS;
- within 0.14, the first Browser -> API Gateway -> Course Service request path has been reasoned and checked;
- within 0.14, API Gateway purpose/routing/business-logic boundary/availability tradeoff has been taught and checked;
- within 0.14, Auth Service identity/authentication ownership and Auth-vs-User/Profile boundary has been taught and checked;
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

- finish 0.14 — First Collaborative Learning Platform HLD one HLD concept at a time under the depth-first teaching rule;
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
- an Enrollment schema/field change should remain an Enrollment implementation detail rather than forcing Payment changes through direct database coupling;
- Enrollment -> Course is a synchronous dependency when Enrollment cannot finish the current student request until Course replies;
- a slow required synchronous dependency contributes directly to the caller's end-to-end latency because the caller is waiting for that result;
- a core business state change such as lesson completion should not fail merely because a secondary notification cannot be delivered immediately;
- asynchronous communication allows a sender to continue without waiting for downstream processing when the business does not require an immediate downstream result;
- a durable messaging mechanism can preserve work while a receiver is temporarily unavailable, reducing temporal coupling between sender and receiver;
- asynchronous processing can create an inconsistency window in which the authoritative service has the new state while a derived downstream view has not caught up yet;
- Course can remain the authoritative source of published-course truth while Search temporarily lags and converges later;
- eventual consistency is a business tradeoff, not a blanket rule: payment-success/enrollment-pending creates materially higher user/business risk than temporary search-index lag;
- user-facing workflow states should describe what has actually happened (for example, payment received / access activation pending) rather than falsely claiming the whole purchase is complete;
- the browser can use the API Gateway as one controlled public backend entry point rather than knowing all internal service endpoints;
- routing decides which downstream service should receive a request while the domain service owns the business rules and result;
- putting service-owned business rules in both Gateway and service creates duplication, inconsistency, coupling, and unnecessary coordinated deployments;
- a Gateway outage can block the browser's normal access path even when downstream services are healthy;
- Course or another domain service needing caller identity does not make it an owner of password verification/authentication;
- Auth should own authentication/security concerns while User/Profile owns profile concerns;
- a single frontend registration screen does not prove that email/password/display-name must have one backend owner;
- duplicated password-validation rules between Gateway and Auth create inconsistent authentication behavior.

Important clarification to preserve: when a downstream service reads caller identity from request context, that identity must already have been established by trusted authentication logic. A raw client-supplied `userId` is not proof of identity.

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

Sections **0.1 through 0.13 are complete as curriculum sections**.

Section **0.14 — First Collaborative Learning Platform HLD is IN PROGRESS**.

Verified 0.14 concepts so far:

1. Browser -> API Gateway -> Course Service request path, Course ownership, and why the course-page interaction is synchronous.
2. API Gateway: controlled public entry point, routing, reduced frontend knowledge of internal service topology, keeping domain business rules out of the Gateway, and Gateway availability tradeoff.
3. Auth Service: identity vs authentication at HLD level, why authentication responsibility should be centralized rather than duplicated across services, Auth-vs-User/Profile separation, and why one frontend workflow does not define one backend service boundary.

Do not treat JWT, access tokens, refresh tokens, OAuth/OIDC, or authorization as already taught. Those concepts were intentionally deferred.

No implementation work has been performed, and Milestone 0 remains in progress.

## Next Engineering Step

No code/infrastructure action yet.

Continue **0.14 — First Collaborative Learning Platform HLD** under the learner-specific depth-first rule.

**Exact next teaching concept:** **User Service / Profile responsibility in the HLD**. Start from the problem of mixing profile data with authentication data, remind that Auth owns authentication/security concerns, derive User Service ownership/non-ownership, use realistic ownership/failure examples, then stop for an understanding check. Do not introduce the next HLD component until the learner answers and explicitly says `next`.

Do not start application coding before the Milestone 0 assignment has been evaluated.

## Session Update Rule

At the end of every substantial learning/building session, update this file with the real current milestone/status, newly implemented work, remaining work, relevant files/components, verification performed, completion-gate state, and one precise **Next Engineering Step**.
