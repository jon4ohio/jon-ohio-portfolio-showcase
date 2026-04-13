# AIUX Process

## Purpose

This document explains the repeatable workflow used to design and ship portfolio updates with AI-assisted tooling while maintaining design quality and implementation discipline.

## Tooling model

- Cursor, Codex, and Claude are used as implementation partners.
- The human owner is responsible for product taste, decision quality, and final acceptance.
- Architectural constraints are documented and enforced through ADRs.

## End-to-end workflow

1. **Define goal + constraints**
   - Clarify user-facing outcome.
   - Lock constraints (e.g., styling conventions, accessibility expectations, responsive requirements).

2. **Explore and compare options**
   - Generate at least two viable approaches.
   - Evaluate trade-offs explicitly (speed, risk, maintainability, consistency).

3. **Record decision**
   - Capture context, options, decision drivers, chosen option, and consequences in an ADR.
   - Include risks, mitigation, and review trigger.

4. **Implement focused changes**
   - Prefer targeted, reversible edits over broad rewrites.
   - Keep blast radius small and scoped to the owning files/components.

5. **Verify outcomes**
   - Check responsive behavior (mobile, tablet, desktop).
   - Check interaction quality (hover/focus/flow).
   - Check accessibility semantics and keyboard behavior.
   - Confirm no regressions in neighboring surfaces.

6. **Curate and publish evidence**
   - Copy high-signal ADRs that contain no private content.
   - Add sanitized snippets that map directly to each ADR.
   - Keep private case-study narrative and assets out of public artifacts.

## Decision quality standards

- One decision per ADR.
- At least two viable options.
- Explicit consequences (positive and trade-offs).
- Operational impact documented.
- Risks include owner + actionable mitigation.

## Verification checklist

- Responsive breakpoints are intentional and testable.
- Interactive states remain visible and consistent.
- Decorative elements do not add assistive-technology noise.
- Metadata and route behavior remain explicit.
- Public artifacts contain no private narrative, assets, or secrets.

## Public showcase policy

- Publish process receipts, not private production source.
- Favor evidence density over volume.
- Keep documents concise, specific, and reproducible.
