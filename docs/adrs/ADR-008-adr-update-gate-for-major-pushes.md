# ADR-008: ADR update gate for major pushes

> **Note:** Abbreviated for the public showcase; full detail lives in the private application repository.

## Status

**Status:** Accepted  
**Date:** 2026-04-10  
**Decision Maker(s):** John Ohio (Owner/Maintainer)  
**Supersedes:** None  

## Context

The project evolves through architecture-affecting pushes (theme system expansion, token governance, interaction model changes). Documenting those changes only from memory creates drift between code and architecture rationale.

**In scope:** What qualifies as a major push, and requiring an ADR creation or update before those pushes are considered complete.  
**Out of scope:** Automating remote push blocking, CI policy, or minor typo/docs-only commits.

## Decision Drivers

- Architecture decisions must remain traceable as code evolves.
- Contributors need consistent decision context without chat history.
- The process must stay lightweight enough to follow on every major push.

## Options Considered

### Option A: Mandatory ADR checkpoint for major pushes (chosen)

- **Description:** A major-push checklist requires an ADR action (new ADR, superseding ADR, or explicit “no ADR needed” note) before the push is treated as complete.
- **Pros:** Consistent governance; low tooling complexity.
- **Cons:** Adds a documentation step to major delivery cadence.

### Option B: Optional ADR updates by maintainer judgment

- **Pros:** No process overhead.
- **Cons:** High risk of architecture drift and lost rationale — **rejected.**

## Decision

**We use Option A.** Every major push must include an ADR action: create a new ADR, supersede an existing ADR, or explicitly document why no ADR change is required.

## Consequences

### Positive

- Major architectural changes stay documented and reviewable.
- The ADR index remains useful for onboarding and audits.

### Negative / Trade-offs

- Small procedural step before finalizing major pushes.
- Index and cross-links must be updated when superseding decisions.

### Risks

| Risk | Likelihood | Impact | Mitigation | Owner | Review Trigger |
|------|------------|--------|------------|-------|------------------|
| Major change ships without an ADR update | Med | High | Major-push checklist in contributor docs and this repo’s README; complete before push | Maintainer | Changes to architecture, tokens, routing, data model, or operational workflow |

## Review Schedule

- **Next review:** 2026-07-10  
- **Review owner:** John Ohio (Owner/Maintainer)  

## Related ADRs

- [ADR-001](ADR-001-inline-styles-for-layout-and-visuals.md) — styling conventions major pushes may affect. Theme and contrast governance decisions in the private repo also interact with this gate.

## References

- This repository’s `README.md` and `docs/maintenance-workflow.md`
- `docs/adrs/index.md`
