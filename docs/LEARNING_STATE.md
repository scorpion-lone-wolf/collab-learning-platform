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
- Course owns course configuration/publishing truth, Payment owns financial transaction/refund truth, Enrollment owns course-entitlement truth, and Learning Progress owns learner-completion truth.

## Partially Understands

- independently discovering bounded contexts from an unfamiliar domain without relying on memorized examples;
- articulating the precise business question a context answers;
- explaining why one responsibility belongs inside a context and another does not;
- turning bounded-context reasoning into a service responsibility map across a whole domain;
- source-of-truth/data ownership across independently deployed services needs deeper practice;
- sync-vs-async decisions have only been introduced conceptually.

## Needs Reinforcement

- repeated cross-domain bounded-context discovery using unfamiliar domains;
- identifying business capability vs entity/table vs workflow;
- defining one-sentence responsibility statements;
- identifying authoritative source-of-truth ownership;
- using business rules, language, cohesion, and reasons-to-change to justify boundaries;
- deciding whether a boundary is only a logical/module boundary or may justify a separate service boundary;
- database-per-service/data ownership implications;
- synchronous vs asynchronous communication tradeoffs.

## Misconceptions / Weak Areas

- bounded-context grouping was initially easier than explaining why a responsibility belongs in one context and not another; this improved through repeated exercises using business question, source of truth, business rules, and reason-to-change reasoning.

## Resolved Misconceptions

- clarified that a monolith does not automatically mean one failure always breaks every capability;
- clarified that microservices do not automatically guarantee failure isolation;
- clarified that Course content ownership is distinct from learner progress ownership;
- clarified that current course price metadata and historical amount actually charged are different business truths owned by different contexts.

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
- correctly separated Course (publish/manage), Payment (purchase/refund), and Enrollment (grant/revoke access) and supplied a business rule for each.

## Assignment History

No milestone assignment has been submitted or graded yet.

## Current Assignment Status

No active milestone assignment yet. The current work is a learner-requested reinforcement block, not the Milestone 0 graded assignment.

## Parking Lot

No deferred topics recorded yet.

## Current Checkpoint

Sections **0.1 through 0.8 are complete as curriculum sections**.

The learner has correctly solved several bounded-context and responsibility-mapping exercises, but has explicitly said they are **not yet confident doing this independently**. Do not infer mastery from section completion. Continue deliberate practice before 0.9.

## Next Teaching Step

Run a **bounded-context and service-boundary reinforcement block before 0.9**.

Use unfamiliar domains (not the Collaborative Learning Platform) so the learner cannot rely on memorized answers. Practice this sequence repeatedly:

1. identify candidate business capabilities;
2. state the business question each candidate context answers;
3. identify the authoritative data/source of truth;
4. identify business rules that belong together;
5. identify different reasons to change;
6. distinguish shared nouns from shared responsibility;
7. map responsibilities into bounded contexts;
8. only then discuss whether each context should remain a module or become a separately deployable service.

Do not start **0.9 — Data ownership and database-per-service** automatically.

After the learner demonstrates stronger independent reasoning, explicitly ask: **"0.9 — Data ownership and database-per-service is next. Do you want to start it now, or continue boundary practice?"**

If a new conversation begins before that choice is made, resume this reinforcement block first and then ask that question.

## Session Update Rule

At the end of every substantial learning session, update this file with:

- newly demonstrated understanding;
- concepts that are only partially understood;
- weak areas or misconceptions;
- completed reasoning checks/assignments and their real verdicts;
- deferred topics worth preserving;
- one precise **Next Teaching Step**.

Keep this file concise enough that a new session can reconstruct the learner's actual position quickly.
