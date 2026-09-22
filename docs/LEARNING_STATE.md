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

- cross-domain bounded-context discovery using unfamiliar domains;
- identifying business capability vs entity/table vs workflow;
- defining one-sentence responsibility statements;
- identifying authoritative source-of-truth ownership;
- using business rules, language, cohesion, and reasons-to-change to justify boundaries;
- deciding whether a boundary is only a logical/module boundary or may justify a separate service boundary;
- database-per-service/data ownership implications;
- synchronous vs asynchronous communication tradeoffs.

These are **reinforcement areas, not blockers for starting 0.9**. Revisit them when useful and use later sections to strengthen the same reasoning skills.

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

No active milestone assignment yet.

## Parking Lot

- Continue bounded-context/responsibility-mapping practice across unfamiliar domains when requested or when later reasoning reveals weakness. This is deliberately deferred and does not block 0.9.

## Current Checkpoint

Sections **0.1 through 0.8 are complete as curriculum sections**.

The learner has correctly solved several bounded-context and responsibility-mapping exercises. Confidence in independently deriving boundaries is still developing, but the learner explicitly chose to proceed rather than make additional practice a prerequisite.

The next formal section is **0.9 — Data ownership and database-per-service**.

## Teaching Approach Requirement

For all future teaching in this project, especially architecture/design topics, do not jump directly to conclusions such as "this is the bounded context" or "this service owns this responsibility."

Show the reasoning path explicitly and step by step:

1. start from the raw requirement/problem;
2. identify the relevant actors and actions;
3. ask what business question is actually being answered;
4. identify the rules and data involved;
5. determine what must stay consistent together;
6. identify the authoritative owner/source of truth;
7. compare plausible alternative groupings;
8. explain why one boundary is better and why the others are weaker;
9. only then name the context/module/service boundary;
10. apply the same reasoning method to new domains so the learner can reproduce the process independently.

This requirement applies across the curriculum, not only to bounded contexts. The learner's goal is to understand and reproduce the design thought process, not memorize final answers.

## Next Teaching Step

Begin **0.9 — Data ownership and database-per-service**.

Teach it from the engineering problem upward and show the full reasoning path rather than presenting ownership rules as conclusions. Connect new data-ownership decisions back to the bounded-context reasoning already learned, and use concrete examples to show why a particular service becomes authoritative for particular data.

Do not require completion of the deferred reinforcement block before 0.9. Preserve the reinforcement need and revisit it naturally when relevant.

## Session Update Rule

At the end of every substantial learning session, update this file with:

- newly demonstrated understanding;
- concepts that are only partially understood;
- weak areas or misconceptions;
- completed reasoning checks/assignments and their real verdicts;
- deferred topics worth preserving;
- one precise **Next Teaching Step**.

Keep this file concise enough that a new session can reconstruct the learner's actual position quickly.
