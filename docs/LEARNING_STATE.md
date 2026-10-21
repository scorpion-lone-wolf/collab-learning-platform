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

The learner has demonstrated understanding of:

- monolith vs modular monolith vs microservice runtime/deployment boundaries;
- why microservices add network uncertainty, partial failure, distributed-state, compatibility, debugging, testing, operational, and security complexity;
- business-capability boundaries and bounded-context reasoning;
- business ownership should follow source of truth, business rules, cohesion, and reasons to change rather than tables/entities alone;
- the same real-world person/course can appear in multiple bounded contexts with different meanings;
- database-per-service as an ownership/access boundary, not necessarily one physical server per service;
- direct cross-service database access creates schema and ownership coupling;
- consumers should use explicit contracts instead of another service's private database or internal statuses;
- synchronous communication means the caller's current operation waits for a required dependency;
- slow synchronous dependencies increase end-to-end request latency;
- asynchronous communication reduces temporal coupling when the current business operation does not require an immediate downstream result;
- durable messaging can preserve work while a consumer is unavailable;
- asynchronous processing can create an eventual-consistency window;
- authoritative state and derived state may temporarily disagree and later converge;
- acceptable inconsistency depends on business impact;
- payment-success/enrollment-pending is more sensitive than temporary Search lag;
- distributed user-facing workflows should expose truthful intermediate states;
- API Gateway can provide one controlled public backend entry point and route requests without owning domain business rules;
- Gateway availability is itself an important runtime dependency;
- identity vs authentication at HLD level;
- Auth Service owns authentication/security concerns rather than profile or unrelated business state;
- User/Profile and Auth can represent the same human for different responsibilities;
- one frontend workflow/screen can involve multiple backend owners;
- duplicating password/authentication rules across Gateway/Auth creates inconsistent security behavior and coupling;
- User Service owns profile information such as display name, bio, preferences, and similar product-facing user information;
- login email should not be independently authoritative in both Auth and User without an explicit different business meaning;
- data being "about a user" does not automatically make it User Service data;
- a raw client-provided `userId` is a claim, not proof of identity;
- downstream services may rely on caller identity only after trusted authentication logic has established it;
- Course Service owns course-management truth: course definition, modules, lessons, publishing state, instructor ownership, current course metadata, and current configured price;
- Payment owns historical amount actually charged, even when the current course price later changes;
- Enrollment owns enrollment/access state;
- Learning Progress owns learner completion/progress state;
- Search can contain a derived searchable representation while Course remains the authoritative owner;
- if Course is published while Search is stale, the course is still published but temporarily not searchable;
- Search catching up later is eventual consistency, not a switch from asynchronous to synchronous communication.

## Partially Understands

- independently discovering bounded contexts from an unfamiliar domain without relying on memorized examples;
- articulating the precise business question a context answers;
- explaining why one responsibility belongs inside a context and another does not;
- turning bounded-context reasoning into a complete service responsibility map across a whole domain;
- deciding whether a logical/module boundary justifies a separate runtime/deployment boundary.

## Needs Reinforcement

- cross-domain bounded-context discovery using unfamiliar domains;
- identifying business capability vs entity/table vs workflow in unfamiliar examples;
- concise one-sentence responsibility statements;
- deeper database-per-service tradeoffs as distributed workflows become more complex;
- preserving the distinction between trusted authenticated request context and arbitrary client-supplied identity data;
- continuing to use precise terminology: asynchronous communication may later converge to consistent state, but does not thereby become synchronous.

These are reinforcement areas, not blockers for the next curriculum concept.

## Misconceptions / Weak Areas

- bounded-context grouping was initially easier than explaining why a responsibility belongs in one context and not another; this improved through repeated exercises using business question, source of truth, business rules, and reason-to-change reasoning;
- briefly described eventual convergence as becoming "sync"; corrected and demonstrated that eventual consistency does not mean asynchronous communication becomes synchronous;
- initially treated "request came from Gateway" as sufficient to trust caller identity; corrected to the stronger rule that trusted authentication logic must first establish the identity.

## Resolved Misconceptions

- a monolith does not automatically mean one failure always breaks every capability;
- microservices do not automatically guarantee failure isolation;
- Course content ownership is distinct from learner progress ownership;
- current course price and historical amount actually charged are different business truths;
- another service needing data does not make it a co-owner of that data;
- one registration form does not imply one backend owner;
- User Service should not automatically duplicate Auth's authoritative login email;
- a raw `userId` supplied by the client is not authentication proof;
- Search lag after Course publication means stale derived state, not failed publication;
- eventual Search catch-up does not make the communication synchronous.

## Completed Understanding Checks

- identified one NestJS application with multiple modules as a monolith;
- identified Enrollment as the owner of enrollment-state changes;
- explained why Payment directly changing Enrollment data creates tight coupling;
- identified shared-database coupling and synchronous request-chain coupling;
- chose to preserve core business success when a non-critical notification fails;
- explained why a timeout is an ambiguous remote outcome and why blind retry may duplicate a charge;
- separated Course, Payment, Enrollment, Auth/Profile, and Learning Progress business truths;
- assigned current Course price to Course, actual charged amount to Payment, and current access entitlement to Enrollment;
- explained why services should use explicit contracts instead of directly querying another service's database;
- identified Enrollment -> Course as synchronous when Enrollment cannot complete without Course's answer;
- explained durable asynchronous messaging and temporal-coupling reduction;
- explained eventual consistency using Course -> Search;
- compared low-impact Search lag with higher-impact payment-success/enrollment-pending;
- completed the 0.13 sync-vs-async reasoning check including recovery/compensation thinking;
- completed the 0.14 Browser -> API Gateway -> Course request-path check;
- completed the API Gateway HLD concept check;
- completed the Auth Service HLD concept check;
- completed the User/Profile Service HLD concept check, including duplicate-email ownership and trusted-identity corrections;
- completed the Course Service HLD concept check, including current-price vs historical-payment ownership, service-field ownership, and Course-authoritative/Search-stale reasoning.

## Assignment History

No milestone assignment has been submitted or graded yet.

## Current Assignment Status

No active milestone assignment yet.

## Parking Lot

- Continue bounded-context/responsibility-mapping practice across unfamiliar domains when requested or when later reasoning reveals weakness.
- At Milestone 25, explicitly teach why/when a standalone Search Service is justified instead of normal Course Service + PostgreSQL search. Start from the simple approach, identify the concrete problems that motivate OpenSearch/separate ownership, cover tradeoffs and when not to split it, then teach OpenSearch from zero.

## Current Checkpoint

Sections **0.1 through 0.13 are complete as curriculum sections**.

Section **0.14 — First Collaborative Learning Platform HLD is IN PROGRESS**.

Completed and demonstrated inside 0.14 so far:

1. Browser -> API Gateway -> Course Service request path and why that interaction is synchronous;
2. API Gateway responsibility and availability tradeoff;
3. Auth Service responsibility and Auth-vs-User/Profile boundary;
4. User Service / Profile responsibility, including authoritative ownership and trusted caller identity;
5. Course Service responsibility, including course-management ownership, current price vs historical payment, separation from Enrollment/Progress/Payment, and Course-authoritative/Search-derived eventual consistency.

No implementation work has been performed.

Do **not** assume JWT, access tokens, refresh tokens, OAuth/OIDC, or authorization have been taught. They remain intentionally deferred.

## Teaching Approach Requirement

For architecture/design topics, continue showing the reasoning path explicitly:

```text
raw problem -> actors/actions -> business question -> rules/data -> consistency needs -> authoritative owner -> alternatives -> boundary choice -> named context/service -> transfer to a new example
```

### Learner-specific depth-first teaching rules — HARD REQUIREMENT

1. Teach **one concept at a time**. Do not introduce the next concept until the learner has answered the understanding questions and explicitly says `next`.
2. Prefer **in-depth teaching over high-level coverage**.
3. Do not skip details because they appear obvious, basic, or implied.
4. Explain unfamiliar technical words in simple English before using them as prerequisites.
5. For each concept, teach in this structure:
   - **The problem**;
   - **The solution**;
   - **Simple real-life example / analogy**;
   - **What goes wrong if we do it the other way**;
   - **Key points for notes**;
   - **One-line summary**.
6. Use short sentences and simple English without reducing technical depth.
7. Explain **why** each design/implementation choice exists.
8. When connecting to an earlier concept, give a one-line reminder.
9. Where relevant, include runtime behavior, failure behavior, alternatives, tradeoffs, production implications, and project application.
10. End each concept with a few understanding questions and wait for the learner's answer.
11. If an answer reveals a gap, re-explain that exact gap before moving on.
12. Do not compress multiple concepts merely to shorten a response.
13. Never treat a broad architecture diagram as proof that each component is understood.

**Depth-over-breadth rule:** when forced to choose between covering more topics quickly and teaching the current concept thoroughly, choose thorough understanding of the current concept.

## Next Teaching Step

**Section 0.14 — First Collaborative Learning Platform HLD remains IN PROGRESS.**

**Exact next teaching step for the next chat:** teach **Enrollment Service responsibility in the HLD** as one concept only.

Start from the problem of confusing three different business facts:

```text
what the course is             -> Course
what happened financially      -> Payment
whether this learner has access -> Enrollment
```

Before using the term **entitlement** as shorthand, explain it simply as "the learner's current right/access to a course." Derive what Enrollment owns and does not own, show why Payment success does not make Payment the owner of access state, include realistic failure/ownership examples, and end with understanding questions.

Do not introduce Learning Progress or another HLD component until the learner answers and explicitly says `next`.

## Session Update Rule

At the end of every substantial learning/building session, update this file with newly demonstrated understanding, partial understanding, weak areas/misconceptions, completed checks/assignments, deferred topics, and one precise **Next Teaching Step**.
