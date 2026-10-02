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
- modular monoliths cannot independently scale one internal module without scaling the whole application;
- microservices introduce network uncertainty, partial failure, distributed state, compatibility, debugging, testing, operational, and security complexity;
- a timeout means the caller did not receive a result in time, not that the remote business operation definitely failed;
- blind retries can duplicate business side effects such as charging a learner twice;
- business data should be modified by the capability/module/service that owns it;
- Payment directly mutating Enrollment data is tight data-ownership coupling;
- a long required service call chain such as Auth -> Course -> Payment creates request/runtime coupling;
- tightly coupled failures can increase blast radius;
- a successful core business operation should not necessarily fail because a non-critical notification dependency fails;
- service boundaries should be reasoned from business capabilities rather than tables or technical layers;
- high business cohesion is a stronger reason to group responsibilities than merely sharing nouns/entities;
- a bounded context groups business concepts, rules, data ownership, and language with one clear responsibility;
- the same real-world person/course can appear in multiple bounded contexts with different meanings;
- Course Management, Payment, Enrollment, Auth/Profile, and Learning Progress own different business truths even when they participate in the same workflow;
- Course owns course configuration/publishing and current-price truth, Payment owns financial transaction/refund and historical-charge truth, Enrollment owns course-entitlement truth, and Learning Progress owns learner-completion truth;
- database-per-service is primarily an ownership/access boundary and does not require a separate physical database server for every service;
- a service should not directly read or modify another service's private database;
- direct cross-service database access couples consumers to the owning service's internal schema and weakens independent evolution/deployment;
- when another service needs owned information, it should obtain it through an explicit service contract rather than bypassing the owner;
- service contracts should expose stable business capabilities/semantics rather than mirror private database rows;
- a consumer should not reinterpret another service's internal status codes or business rules;
- internal schema changes should not require consumer changes when the external contract remains compatible;
- Payment can communicate refund outcome, but Enrollment remains responsible for deciding and applying course-access changes;
- a service interaction is synchronous when the caller's current operation cannot complete until a required dependency responds;
- a slow required synchronous dependency increases the caller's end-to-end latency because the caller is waiting for that dependency's result;
- asynchronous communication allows a sender to continue without waiting for the receiver to complete when the current business operation does not require that immediate result;
- durable messaging can preserve a message while a consumer/receiver is temporarily unavailable;
- asynchronous messaging reduces temporal coupling because producer and consumer do not have to be available at the same time;
- asynchronous communication does not remove failure; it changes the failure boundary and introduces messaging, delayed-processing, retry, duplicate-processing, and operational concerns;
- eventual consistency means related representations may temporarily disagree and later converge when downstream processing completes;
- the authoritative service remains the source of truth while a derived downstream view may temporarily lag;
- the acceptable inconsistency window is a business/operational decision and depends on impact;
- search-index lag is generally lower impact than a paid learner waiting for enrollment/access;
- distributed user-facing workflows should expose honest intermediate states such as payment received / access activation pending rather than claiming completion before all required business outcomes have occurred.

## Partially Understands

- independently discovering bounded contexts from an unfamiliar domain without relying on memorized examples;
- articulating the precise business question a context answers;
- explaining why one responsibility belongs inside a context and another does not;
- turning bounded-context reasoning into a service responsibility map across a whole domain;
- sync-vs-async decision-making using immediate business dependency, acceptable inconsistency windows, failure coupling, latency coupling, user-visible intermediate states, and recovery/compensation requirements.

## Needs Reinforcement

- cross-domain bounded-context discovery using unfamiliar domains;
- identifying business capability vs entity/table vs workflow;
- defining one-sentence responsibility statements;
- using business rules, language, cohesion, and reasons-to-change to justify boundaries;
- deciding whether a boundary is only a logical/module boundary or may justify a separate service boundary;
- deeper database-per-service tradeoffs as they appear in later distributed workflows;
- synchronous vs asynchronous communication tradeoffs.

These are reinforcement areas, not blockers for the next curriculum section.

## Misconceptions / Weak Areas

- bounded-context grouping was initially easier than explaining why a responsibility belongs in one context and not another; this improved through repeated exercises using business question, source of truth, business rules, and reason-to-change reasoning.

## Resolved Misconceptions

- clarified that a monolith does not automatically mean one failure always breaks every capability;
- clarified that microservices do not automatically guarantee failure isolation;
- clarified that Course content ownership is distinct from learner progress ownership;
- clarified that current course price metadata and historical amount actually charged are different business truths owned by different contexts;
- demonstrated that another service needing data does not make it a co-owner of that data.

## Completed Understanding Checks

- identified one NestJS application with multiple modules as a monolith;
- identified Enrollment as the owner of enrollment-state changes;
- explained why Payment directly changing Enrollment data creates tight coupling;
- identified shared-database coupling and request-chain coupling in a nominal microservice setup;
- chose to preserve enrollment success when notification delivery fails and justified the business reason;
- explained why a payment timeout is an ambiguous outcome and why blind retry can double-charge;
- grouped Course creation/lesson/publishing responsibilities separately from Payment;
- separated Auth credential/security responsibilities from Profile responsibilities;
- separated Enrollment entitlement from Learning Progress;
- correctly separated Course (publish/manage), Payment (purchase/refund), and Enrollment (grant/revoke access);
- for 0.9, correctly assigned current Course price to Course, actual historical charged amount to Payment, and current access entitlement to Enrollment;
- explained that Payment should use an explicit service contract rather than directly SELECT from Enrollment's private database, citing ownership and schema-coupling consequences;
- identified a contract that exposed entire Course/Payment internal rows as over-coupled and recognized leaked business-rule interpretation;
- designed smaller business-oriented contracts and explained why internal database-column changes should not affect consumers;
- correctly reasoned that Payment should not directly revoke Enrollment-owned access after a refund;
- identified Enrollment -> Course as synchronous when Enrollment cannot answer until Course replies;
- explained that if Course becomes slow, Enrollment and therefore the student's overall request become slower because the dependency's latency contributes to end-to-end latency;
- correctly kept Lesson completion successful even when achievement-email delivery is unavailable, because Learning Progress owns the core state change;
- explained that a durable messaging mechanism can retain work while a downstream receiver is unavailable and allow the sender to continue;
- distinguished synchronous waiting from asynchronous sender/receiver decoupling;
- correctly reasoned that Course publication can succeed while Search is down when the business tolerates delayed discoverability;
- identified the temporary disagreement between Course state and Search state as eventual consistency and explained that Search later catches up;
- identified payment-success/enrollment-pending as eventual consistency with higher business impact because a learner may have paid without receiving access;
- proposed an explicit pending-access user experience after payment rather than pretending the full purchase workflow has already completed.
- completed the 0.13 final reasoning check: kept Payment success separate from Enrollment completion, chose an honest pending-access UI state, described later Enrollment recovery, and identified compensation/refund for an unrecoverable enrollment failure.

## Assignment History

No milestone assignment has been submitted or graded yet.

## Current Assignment Status

No active milestone assignment yet.

## Parking Lot

- Continue bounded-context/responsibility-mapping practice across unfamiliar domains when requested or when later reasoning reveals weakness.
- At Milestone 25, explicitly teach why/when a standalone Search Service is justified instead of normal Course Service + PostgreSQL search. Start from the simple approach, identify the concrete problems that motivate OpenSearch/separate ownership, cover tradeoffs and when not to split it, then teach OpenSearch from zero.

## Current Checkpoint

Sections **0.1 through 0.12 are complete as curriculum sections**.

The learner demonstrated the core 0.9 ownership rule and the reason database privacy matters for independent service evolution. The learner also demonstrated the core 0.10 contract principle: consumers should depend on explicit, stable business semantics rather than another service's storage model or internal status codes. In 0.11, the learner correctly identified synchronous request dependency and explained how dependency latency affects the caller's end-to-end request latency. In 0.12, the learner correctly explained asynchronous sender/receiver decoupling, durable messaging, temporal coupling reduction, eventual consistency, authoritative-vs-derived state, and the difference in business impact between delayed Search indexing and delayed Enrollment after payment.

## Teaching Approach Requirement

For architecture/design topics, continue showing the reasoning path explicitly: raw problem -> actors/actions -> business question -> rules/data -> consistency needs -> authoritative owner -> alternatives -> boundary choice -> named context/service -> transfer to a new example.

## Next Teaching Step

**Section 0.13 — Sync vs async decision-making is complete.** The learner demonstrated that: Payment can complete its own payment state and publish `PaymentSucceeded` without waiting synchronously for Enrollment; the UI must show an honest intermediate state such as payment received / access activation pending; Enrollment should process the durable event when it recovers; and a permanently failed enrollment may require compensation such as a refund and reversal of other dependent state changes.

**Next Teaching Step:** begin **0.14 — First Collaborative Learning Platform HLD**. Start by turning the boundaries and sync/async rules learned so far into the first system-level diagram: client/edge, core services, owned data, and the major synchronous vs asynchronous paths. Explain each box and arrow before adding the next one.

## Session Update Rule

At the end of every substantial learning session, update this file with newly demonstrated understanding, partial understanding, weak areas/misconceptions, completed checks/assignments, deferred topics, and one precise **Next Teaching Step**.
