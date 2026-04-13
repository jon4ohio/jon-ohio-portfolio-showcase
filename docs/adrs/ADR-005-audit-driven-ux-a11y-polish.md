# ADR-005: Audit-driven UX and accessibility polish via targeted in-place fixes

## Status

**Status:** Accepted
**Date:** 2026-04-09
**Decision Maker(s):** John Ohio (Owner/Maintainer)
**Supersedes:** None

## Context

An audit of the portfolio surfaced interaction, accessibility, and responsive behavior issues across navigation, footer links, case studies, and supporting layouts. The issues were narrow and implementation-level (hover feedback, decorative semantics, breakpoint behavior, not-found metadata, content order), but they created visible UX friction and accessibility noise.

The project already has accepted constraints from prior ADRs:
- Layout and visual styling stay primarily inline (ADR-001).
- Responsive behavior is handled through focused utility classes in `app/globals.css` (ADR-003).

The decision needed now was whether to resolve the audit as incremental code-level improvements in existing structures, or redesign/refactor broader UI patterns first.

**In scope:** targeted UX/a11y/layout fixes from the audit (hover affordance, aria attributes for decorative separators/elements, not-found metadata/page, mobile/tablet layout corrections, case-study content flow order); color token migration; homepage polish (systems row layout, spacing normalization, section contrast improvements)
**Out of scope:** comprehensive visual redesign, data model changes, removing optional project fields

## Decision Drivers

- Resolve concrete UX/a11y regressions quickly without redesign churn
- Preserve accepted architecture conventions from ADR-001 and ADR-003
- Keep risk low by preferring localized, reviewable changes over broad rewrites
- Ensure metadata and accessibility semantics are explicit and testable

## Options Considered

### Option A: Targeted in-place fixes in current components and CSS utilities

- **Description:** Apply focused updates in affected files using existing conventions: add hover states, aria semantics, not-found metadata/page, specific breakpoint tweaks, and case-study content reordering. Keep changes localized to responsible files and utility classes.
- **Pros:**
  - Fastest path to remove user-visible friction and accessibility noise
  - Low blast radius and straightforward review/verification
  - Fully compatible with ADR-001 and ADR-003
  - Easier rollback if any single fix has side effects
- **Cons:**
  - Some style repetition remains until later refactor passes
  - Produces incremental improvements rather than a unified redesign pass
- **Effort:** Low
- **Notes:** Aligns with the audit nature (targeted issues, not structural redesign).

### Option B: Full pattern redesign and component consolidation before fixing audit items

- **Description:** Redesign shared UI patterns (nav, metadata rows, section headers, cards) and consolidate styles/components first, then absorb audit fixes into the larger redesign.
- **Pros:**
  - Could improve long-term consistency in one coordinated effort
  - Reduces repeated style patterns more aggressively
- **Cons:**
  - High scope and higher regression risk for a content-led portfolio
  - Slower path to fixing concrete accessibility and interaction issues
  - Harder to review because bug fixes and redesign intent are coupled
- **Effort:** High
- **Notes:** Better as a future redesign ADR if needed.

## Decision

**We will use Option A because it resolves audit findings quickly and safely while preserving existing architectural constraints.**

Implementation makes targeted in-place fixes to interaction feedback, decorative semantics, metadata completeness, responsive behavior, and case-study content flow.

## Consequences

### Positive

- Navigation/footer/work/case-study interactions provide clearer hover affordance
- Decorative separators and device-frame dots are hidden from assistive technologies
- Not-found route has explicit metadata and intentional page output
- Mobile/tablet behavior improves in system model, leadership cards, and about timeline
- Case-study tags appear after visual evidence, improving information flow
- Raw hex colors were replaced with semantic CSS variables
- Systems rows stack title/subtitle above metric badges for narrow viewports
- Section contrast is clearer via full-width surface banding where appropriate

### Negative / Trade-offs

- Styling consistency still relies on a mix of inline styles and utility classes
- Minor UX improvements are distributed across multiple files, requiring careful review
- Color migration adds dependency on CSS custom properties (acceptable for modern browser targets)

### Operational Impact

- Keep future UX/a11y fixes localized to owning components and `app/globals.css`
- Use existing CSS variables before adding new tokens
- Require manual responsive and accessibility spot checks after similar changes
- **Migration / rollback:** each fix is independently reversible without rolling back unrelated improvements

### Risks

| Risk | Likelihood | Impact | Mitigation | Owner/Role | Review Trigger |
|------|-----------|--------|------------|------------|----------------|
| Hover/spacing tweaks unintentionally alter visual hierarchy at specific breakpoints | Med | Med | Require desktop/tablet/mobile checks and constrain selectors to explicit classes | Maintainer | Any shared-selector CSS change |
| Not-found metadata diverges from route metadata conventions | Low | Low | Keep explicit metadata in not-found route and verify title/robots behavior | Maintainer | Any metadata or routing update touching not-found |

## Review Schedule

- **Next review:** 2026-07-01
- **Review owner:** John Ohio (Owner/Maintainer)

## Related ADRs

- ADR-001 — constrains styling approach used by these fixes
- ADR-003 — constrains responsive utility and breakpoint strategy used by these fixes
- ADR-004 — complements prior UI consistency work (metric badges/work layout)

## References

- `app/globals.css`
- `components/Nav.tsx`
- `components/Footer.tsx`
- `components/SystemModel.tsx`
- `components/AssetImage.tsx`
- `app/not-found.tsx`
- `app/work/page.tsx`
- `app/work/[slug]/page.tsx`
- `app/leadership/page.tsx`
- `app/about/page.tsx`
- `app/page.tsx`
