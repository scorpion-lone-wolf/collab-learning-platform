# Architecture Decisions

> **Purpose:** Preserve durable architecture and engineering decisions for the Collaborative Learning Platform so later sessions can understand not only **what** was chosen, but **why**.

## Decision Recording Rules

Record an ADR when a decision is durable enough that future milestones may depend on it, for example:

- service boundaries;
- database/data ownership;
- synchronous vs asynchronous communication choices;
- API/event contract strategy;
- authentication/authorization strategy;
- persistence strategy;
- major infrastructure choices;
- security boundaries;
- deployment/operational choices;
- important tradeoffs that should not be re-decided accidentally.

Do **not** create an ADR for every code edit, command, package installation, or temporary experiment.

`MASTER_CURRICULUM.md` defines the learning scope and target technologies. This file records project decisions when they are actually discussed and justified; do not invent learner decisions merely because a technology appears in the curriculum.

## ADR Status Values

Use one of:

- **Proposed** — under consideration; not yet adopted.
- **Accepted** — current decision.
- **Deprecated** — still historically relevant but should no longer be used for new work.
- **Superseded** — replaced by another ADR; keep the old record and link to its replacement.
- **Rejected** — considered but intentionally not chosen.

## Decision Index

No project-specific architecture decisions have been recorded yet.

The first ADRs are expected to emerge during **Milestone 0 — Architecture Orientation and System HLD**, after the relevant tradeoffs have been taught and discussed.

---

# ADR Template

Copy this template when a real durable decision is made.

```markdown
## ADR-NNN — <Short Decision Title>

**Status:** Proposed / Accepted / Deprecated / Superseded / Rejected

**Date:** YYYY-MM-DD

**Milestone:** Milestone N — <name>

### Context

What engineering problem or constraint requires a decision?

### Decision

What are we choosing?

### Reason

Why is this the best choice for this project at this point?

### Alternatives Considered

- Alternative A — why it was not chosen.
- Alternative B — why it was not chosen.

### Tradeoffs / Consequences

Positive and negative consequences of the decision.

### Follow-up / Revisit Conditions

What future evidence, scale, requirement, or milestone would justify revisiting this decision?

### Supersedes / Superseded By

Only when applicable.
```

## Preservation Rule

Never silently delete or rewrite an accepted historical decision because the architecture later changes.

If a decision changes:

1. preserve the old ADR;
2. mark its status appropriately, usually **Superseded** or **Deprecated**;
3. create a new ADR for the replacement decision;
4. cross-reference the old and new ADRs.
