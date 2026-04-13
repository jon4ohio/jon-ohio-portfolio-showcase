# ADR-004: Shared metric-badge CSS, work index grid, and local preview in Cursor

## Status

**Status:** Accepted
**Date:** 2026-04-09
**Decision Maker(s):** John Ohio (Owner/Maintainer)
**Supersedes:** None

## Context

Following ADR-001 (inline styles) and ADR-003 (responsive layout utilities in `globals.css`), the case study hero and work index were updated to use shared metric "pill" styles, a responsive grid for work-list rows, and stacked hero CTAs on small viewports. Purely inline styles would duplicate fluid typography and wrapping rules across pages.

Contributors also need a reliable way to open a live preview while running `npm run dev` inside Cursor/VS Code (Simple Browser, embedded browser, or system browser).

**In scope:** CSS classes for metric badges and related layout hooks; workspace port preview behavior for the Next.js dev server
**Out of scope:** changing data layer; production hosting; CI

## Decision Drivers

- Avoid duplicating the same badge markup and `clamp()` typography in multiple TSX files
- Keep ADR-001 rule: no Tailwind for structural layout; shared primitives live in `globals.css` alongside existing utilities
- Respect responsive/adaptive behavior: wrapping badges, `min-width: 0` on grid children, fluid type
- One-command local preview aligned with `localhost:3000`

## Options Considered

### Option A: Shared CSS classes in `globals.css` + workspace `portsAttributes`

- **Description:** Add `.metric-badges`, `.metric-badge`, `.metric-badge__value`, `.metric-badge__label`, and modifiers (e.g. `.metric-badges--hero`). Keep page-specific spacing via minimal inline style where needed. Add workspace settings with `portsAttributes` for port 3000 and `onAutoForward: "openBrowser"` so the editor can offer open-in-browser actions when the dev server listens.
- **Pros:** DRY badge styling; fluid type in one place; standard VS Code/Cursor port metadata; no new dependencies
- **Cons:** Slight split between class-based chrome and inline spacing (same pattern as ADR-003 grids)
- **Effort:** Low
- **Notes:** Port auto-forward behavior depends on editor port detection; users can still open `http://localhost:3000` manually.

### Option B: Inline-only badges + no workspace port config

- **Description:** Repeat full badge style objects on every page and rely on docs only for preview URLs.
- **Pros:** Maximizes ADR-001 literalism
- **Cons:** Duplication; drift in font sizes; no editor hint for port 3000
- **Effort:** Low ongoing, higher maintenance
- **Notes:** Rejected for maintainability and consistency with ADR-003 utility-class approach.

### Option C: Tailwind component classes for badges

- **Description:** Use Tailwind `@apply` or utility classes for pills.
- **Cons:** Conflicts with ADR-001; unnecessary for two call sites
- **Effort:** Medium
- **Notes:** Rejected.

## Decision

**We will use Option A:** shared metric-badge classes and related utilities in `app/globals.css`, retain existing work-list and hero CTA rules there, and commit workspace settings for port 3000 so Cursor/VS Code can surface preview actions when the Next.js dev server is running.

## Consequences

### Positive

- Metric pills stay visually consistent and scale with `clamp()` on narrow viewports
- Work-list grid and hero CTA breakpoints remain centralized in `globals.css`
- Workspace settings document the canonical dev port for tooling

### Negative / Trade-offs

- Badge spacing (margins) may still be set inline next to `className`; large layout changes can require edits in two places
- `portsAttributes` behavior varies by editor version; not all environments auto-open a browser

### Operational Impact

- **Local preview:** run `npm run dev`, then use Ports view (`Forward Port` / `Open in Browser`) if needed, or open `http://localhost:3000` manually
- **Onboarding:** see project command docs
- **Migration / rollback:** remove workspace port settings if team standardizes on another preview flow; badge classes can be inlined again at the cost of duplication

### Risks

| Risk | Likelihood | Impact | Mitigation | Owner/Role | Review Trigger |
|------|------------|--------|------------|------------|----------------|
| Editor does not auto-open preview despite `portsAttributes` | Med | Low | Document manual Simple Browser URL in project docs | Maintainer | Editor upgrade changes port UI |
| Shared badge classes diverge from page intent | Low | Med | Keep presentation in CSS and copy/spacing intent in TSX | Maintainer | New case study layouts |

## Review Schedule

- **Next review:** 2026-07-01
- **Review owner:** Maintainer

## Related ADRs

- ADR-001 — constrains: no Tailwind for structural layout
- ADR-003 — complements: responsive grids and utilities continue in `globals.css`
- ADR-002 — unaffected

## References

- `app/globals.css` — metric badges, work-list rows, hero CTA rules
- `.vscode/settings.json` — `portsAttributes` for port 3000
- `app/work/[slug]/page.tsx`, `app/work/page.tsx` — usage surfaces
