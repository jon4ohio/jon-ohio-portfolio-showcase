# ADR-023: Figma MCP handoff — map design output to design tokens (no raw hex as source of truth)

> **Note:** Abbreviated for the public showcase; full detail lives in the private application repository.

## Status

**Status:** Accepted  
**Date:** 2026-04-11  
**Decision Maker(s):** John Ohio (Owner/Maintainer)  
**Supersedes:** None  

## Context

The portfolio uses **inline styles** and **CSS custom properties** for design tokens (see [ADR-001](ADR-001-inline-styles-for-layout-and-visuals.md)). Figma MCP tools such as **`get_design_context`** emit **reference** code that often includes **literal hex/RGB** and framework-style classes, even when Figma frames use variables. Imports from design-to-code flows can also flatten appearance to non-token layers. Without a documented rule, changes risk **token drift**, broken **theme** behaviour (e.g. warm/light/dark), and duplicate color sources (hex in components vs variables in global CSS).

**In scope:** Process for Figma → repository handoff; treating MCP output as reference, not final implementation.  
**Out of scope:** Changing MCP or Figma product behaviour; a full ESLint ban on every hex literal (optional later).

## Decision Drivers

- **Theme correctness:** Colours should resolve through **semantic CSS variables** (e.g. `var(--jop-…)` in the private app) so theme switching continues to work.
- **Single source of truth:** Avoid parallel palettes (pasted hex vs tokens).
- **Reviewability:** Reviewers can flag literal colours that bypass tokens.
- **Alignment with ADR-001:** MCP output must be adapted to the project’s styling approach, not pasted wholesale.

## Options Considered

### Option A: Document handoff + checklist; map hex → tokens manually (chosen)

- **Description:** Authoritative rules live in private extended docs; in review, treat MCP output as **reference only** and replace literal colours with **token-backed** `var(...)` values unless an exception is justified.
- **Pros:** Low tooling cost; fits agent and human workflows; no build pipeline change.
- **Cons:** Relies on implementer and reviewer discipline.

### Option B: ESLint rule banning hex in app source

- **Pros:** Stronger enforcement.
- **Cons:** False positives and maintenance — **deferred** unless token violations recur often.

### Option C: One paragraph in contributor docs only (no structured checklist)

- **Cons:** Harder to discover — **rejected** in favour of Option A.

## Decision

**We use Option A.** Implementations derived from **`get_design_context`** (or similar) must **not** treat pasted hex as final styling. Map literals to the project’s **CSS variable / token** system. Case study content and structure remain in the app’s **static data layer** in the private repo (not duplicated here).

### Public handoff checklist (summary)

1. Treat Figma MCP output as **starting reference**, not a merge-ready paste.
2. Replace **hex/RGB in style props** with **semantic tokens** (`var(--jop-…)` or the project’s documented equivalents).
3. Preserve **theme behaviour**: no hard-coded colours that bypass `data-theme` or equivalent.
4. Reconcile **duplicated** colour sources — globals/tokens win over inline literals.
5. For large visual imports, **review** with the same bar as a normal UI PR.

## Consequences

### Positive

- Clear review expectation: token mapping is explicit, not implicit taste.
- Reinforces [ADR-001](ADR-001-inline-styles-for-layout-and-visuals.md) for Figma-driven work.

### Negative / Trade-offs

- Manual mapping adds implementation time — offset by a finite token set and checklist.

### Risks

| Risk | Likelihood | Impact | Mitigation | Owner | Review Trigger |
|------|------------|--------|------------|-------|------------------|
| MCP snippet merged with hex “to ship faster,” breaking theme parity | Med | Med | Checklist + PR review; cite this ADR when importing from Figma MCP | Maintainer | PR that cites Figma MCP or large visual diff from design import |

## Review Schedule

- **Next review:** 2027-01-01 (or when MCP codegen reliably emits token variables).  
- **Review owner:** Maintainer  

## Related ADRs

- [ADR-001](ADR-001-inline-styles-for-layout-and-visuals.md) — inline styles; MCP output must be adapted, not pasted wholesale.  
- Static case-study data and extended theme docs remain in the private repository; this ADR governs **how** Figma-derived UI is reconciled with tokens.

## References

- Private app: `CLAUDE.md`, `docs/figma-jop-structure.md`, and theme token documentation (not mirrored in this showcase).
