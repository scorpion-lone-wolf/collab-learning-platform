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

Curriculum sections **0.1 through 0.13 are complete**:

- 0.1 — Engineering problem / architecture pressures;
- 0.2 — Monolith;
- 0.3 — Modular monolith;
- 0.4 — Microservices;
- 0.5 — Monolith vs modular monolith vs microservices;
- 0.6 — Why microservices are difficult;
- 0.7 — Business capabilities and bounded contexts;
- 0.8 — Service responsibility mapping foundations;
- 0.9 — Data ownership and database-per-service;
- 0.10 — Service contracts;
- 0.11 — Synchronous communication;
- 0.12 — Asynchronous communication;
- 0.13 — Sync vs async decision-making.

Section **0.14 — First Collaborative Learning Platform HLD is IN PROGRESS**.

Verified 0.14 concepts so far:

1. **Browser -> API Gateway -> Course Service request path**
   - Course owns current course information;
   - the page-load interaction is synchronous because the browser needs the result for the current response.
2. **API Gateway**
   - controlled public backend entry point;
   - routing responsibility;
   - reduced frontend knowledge of internal topology;
   - service-owned business rules stay out of the Gateway;
   - Gateway availability is an important runtime dependency.
3. **Auth Service**
   - identity vs authentication at HLD level;
   - Auth owns authentication/security concerns;
   - one frontend workflow does not define one backend boundary;
   - Auth and User/Profile represent the same human for different responsibilities.
4. **User Service / Profile responsibility**
   - User owns profile information such as display name/bio/preferences rather than authentication secrets;
   - the authoritative login email should not be independently owned by both Auth and User without an explicit different business meaning;
   - data being "about a user" does not automatically make it User Service data;
   - a raw client-supplied `userId` is only a claim, not proof of identity;
   - downstream services may use identity only after trusted authentication logic has established it.
5. **Course Service responsibility**
   - Course owns course-management truth: course definition, modules, lessons, publishing state, instructor ownership, and current configured course metadata/price;
   - Payment owns historical amount actually charged;
   - Enrollment owns enrollment/access state;
   - Learning Progress owns learner completion/progress;
   - Search may hold a derived searchable representation but Course remains authoritative;
   - when Course is published but Search has not indexed it yet, the course is published and Search is temporarily stale;
   - Search catching up later is eventual consistency and does not make the communication synchronous.
6. **Enrollment Service responsibility**
   - Enrollment owns the learner-course relationship and the learner's current right/access to a course;
   - Payment success may trigger enrollment work but does not make Payment the owner of access state;
   - access can exist without a payment, such as free or manually granted access;
   - Payment must not directly write Enrollment-owned data because that breaks data ownership and creates schema/business coupling.
7. **Learning Progress Service responsibility**
   - Learning Progress owns lesson completion, course-completion percentage, checkpoints, and learner progress history;
   - Enrollment answers whether a learner may access a course, while Learning Progress answers what the learner has completed;
   - an active enrollment with 0% progress is valid;
   - revoking enrollment does not inherently erase historical progress;
   - Course remains the owner of course structure such as modules and lessons.

8. **Payment Service responsibility**
   - Payment owns the historical financial truth: actual amount charged, payment attempts/outcomes, and refund outcomes;
   - Course owns current configured price; later price changes do not rewrite historical payments;
   - Payment success may trigger but does not own enrollment/access changes;
   - refund financial state is Payment-owned, while any resulting access revocation is Enrollment-owned;
   - temporary cross-service inconsistency requires reliable coordination and recovery, not merely an assumption that an event will arrive.

Previously established architecture foundations remain valid:

- module boundary vs runtime/deployment boundary;
- ownership and coupling basics;
- failure propagation / blast-radius basics;
- shared data access weakens service independence;
- long synchronous dependency chains create request coupling;
- distributed-monolith warning signs;
- business-capability decomposition;
- bounded-context reasoning using responsibility, source of truth, business rules, cohesion, and reasons to change;
- database-per-service as a logical ownership/access boundary, not necessarily one physical database server per service;
- direct cross-service database access creates schema and ownership coupling.

## Still Pending

Continue the established Milestone 0 lesson sequence exactly:

- finish **0.14 — First Collaborative Learning Platform HLD** one HLD concept at a time under the depth-first teaching rule;
  - next: Notification Service responsibility;
  - then continue remaining major HLD components one at a time, including File, Search, Chat, and AI/RAG responsibilities and the important arrows/dependencies between them;
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

The learner has correctly reasoned that:

- one deployable NestJS application with multiple modules is still one monolith;
- Enrollment should own enrollment-state changes rather than Payment mutating Enrollment data directly;
- shared database access creates data-ownership coupling;
- required synchronous service chains create request/runtime and latency coupling;
- a timeout does not prove a remote business operation failed;
- blind retries can duplicate side effects such as charging twice;
- non-critical downstream work such as notification delivery should not automatically invalidate a successful core state change;
- Course Management, Payment, Enrollment, Auth/Profile, and Learning Progress own different business truths;
- Course owns current course pricing/configuration truth, while Payment owns historical amount actually charged;
- another service needing owned information does not make it a co-owner and should use an explicit contract rather than direct database access;
- durable asynchronous messaging can reduce temporal coupling while introducing delayed processing and eventual-consistency concerns;
- Course can remain authoritative while Search temporarily lags and converges later;
- payment-success/enrollment-pending is a higher-risk inconsistency than temporary search lag and should be represented honestly to the user;
- Gateway routing is distinct from domain business logic;
- Auth owns authentication/security concerns while User owns profile concerns;
- one registration screen can involve multiple service owners;
- duplicating authoritative login email across Auth/User creates unclear ownership and synchronization pressure;
- raw client-provided identity is not authentication proof;
- User Service may rely on identity only after trusted authentication logic establishes it;
- Course Service owns course structure and publishing, not enrollment, learner progress, or payment state;
- Search is a derived model and may be temporarily stale after Course publishes;
- asynchronous Course -> Search processing can recover later without turning the interaction into a synchronous dependency;
- Payment success and Enrollment access are related facts but remain separately owned;
- free access demonstrates that Enrollment cannot be modeled as merely a Payment sub-state;
- Payment directly writing Enrollment's database would create ownership/schema coupling;
- Enrollment can be active while Learning Progress is 0%;
- Enrollment revocation and historical learning progress are separate facts;
- Course owns modules/lessons while Learning Progress owns a learner's completion of those lessons;
- Course owns current pricing while Payment owns the historically charged amount, even after the instructor changes the price;
- payment success and an enrollment not yet created are distinct service-owned facts;
- financial refund facts belong to Payment while access revocation, if required, belongs to Enrollment;
- direct Payment access to Enrollment's database would violate service ownership.

Reinforcement for the next lessons: eventual consistency is the desired outcome, not an automatic guarantee; reliable messaging/retries/recovery will be needed to reach convergence after failures.

Important clarification to preserve: when a downstream service reads caller identity from request context, that identity must already have been established by trusted authentication logic. A raw client-supplied `userId` is not proof of identity.

Do not treat JWT, access tokens, refresh tokens, OAuth/OIDC, or authorization as already taught. Those concepts were intentionally deferred.

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

Section **0.14 — First Collaborative Learning Platform HLD remains IN PROGRESS**.

The latest completed concept is **Payment Service responsibility in the HLD**. Enrollment Service, Learning Progress Service, and Payment Service concept checks have all passed.

No implementation work has been performed, and Milestone 0 remains in progress.

## Next Engineering Step

No code/infrastructure action yet.

Continue **0.14 — First Collaborative Learning Platform HLD** under the learner-specific depth-first rule.

**Exact next teaching concept:** **Notification Service responsibility in the HLD**. Start with a learning-platform event such as course enrollment or payment completion and explain why delivery of email/push/in-app messages is a different business capability from the authoritative course, payment, or enrollment facts. Cover what Notification owns and does not own, the consequence of notification failure, and when asynchronous messaging helps at a high level. End with understanding questions. Do not introduce File or another HLD component until the learner answers and explicitly says `next`.

Do not start application coding before the Milestone 0 assignment has been evaluated.

## Session Update Rule

At the end of every substantial learning/building session, update this file with the real current milestone/status, newly implemented work, remaining work, relevant files/components, verification performed, completion-gate state, and one precise **Next Engineering Step**.
