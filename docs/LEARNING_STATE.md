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
- Payment can communicate refund outcome, but Enrollment remains responsible for deciding and applying course-access changes.

## Partially Understands

- independently discovering bounded contexts from an unfamiliar domain without relying on memorized examples;
- articulating the precise business question a context answers;
- explaining why one responsibility belongs inside a context and another does not;
- turning bounded-context reasoning into a service responsibility map across a whole domain;
- synchronous vs asynchronous communication has only been introduced conceptually and is the next area to develop.

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
- correctly reasoned that Payment should not directly revoke Enrollment-owned access after a refund.

## Assignment History

No milestone assignment has been submitted or graded yet.

## Current Assignment Status

No active milestone assignment yet.

## Parking Lot

- Continue bounded-context/responsibility-mapping practice across unfamiliar domains when requested or when later reasoning reveals weakness.

## Current Checkpoint

Sections **0.1 through 0.10 are complete as curriculum sections**.

The learner demonstrated the core 0.9 ownership rule and the reason database privacy matters for independent service evolution. The learner also demonstrated the core 0.10 contract principle: consumers should depend on explicit, stable business semantics rather than another service's storage model or internal status codes.

## Teaching Approach Requirement

For architecture/design topics, continue showing the reasoning path explicitly: raw problem -> actors/actions -> business question -> rules/data -> consistency needs -> authoritative owner -> alternatives -> boundary choice -> named context/service -> transfer to a new example.

## Next Teaching Step

Begin **0.11 — Synchronous communication**.

Start from the engineering problem: when a caller needs an answer before it can continue, explain request/response coupling, availability dependency, latency, timeouts, and failure propagation before introducing concrete HTTP implementation details.

## Session Update Rule

At the end of every substantial learning session, update this file with newly demonstrated understanding, partial understanding, weak areas/misconceptions, completed checks/assignments, deferred topics, and one precise **Next Teaching Step**.
