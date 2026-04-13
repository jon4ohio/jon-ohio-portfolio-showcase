# John Ohio Portfolio - Public Showcase

This repository is a curated, public-facing showcase of how I built my portfolio using an AI-assisted design/engineering workflow.

The production site is live at:
- https://jonohio.vercel.app

## What this repo is

- A process and decision record (not the private source-of-truth app repo).
- A transparent view into how product/UX decisions were made.
- A small set of sanitized, non-runnable code snippets that illustrate implementation patterns.

## What this repo is not

- Not the complete application source code.
- Not a copy of private case-study content or assets.
- Not a full commit-by-commit development history.

## AIUX Workflow

I collaborate with agentic tools (Cursor, Codex, Claude) to ship design-quality frontend work:

1. Define constraints and goals.
2. Evaluate options and trade-offs.
3. Capture decisions in ADRs.
4. Implement focused changes.
5. Verify UX/accessibility/responsive outcomes.
6. Document consequences and operational impact.

For a deeper walkthrough, see `docs/aiux-process.md`.

## Receipts

- Decision records: `docs/adrs/`
- Sanitized implementation evidence: `snippets/`

Suggested reading order:
1. `docs/adrs/ADR-001-inline-styles-for-layout-and-visuals.md`
2. `docs/adrs/ADR-003-responsive-layout-via-css-utility-classes.md`
3. `docs/adrs/ADR-004-shared-metric-badges-work-grid-cursor-preview.md`
4. `docs/adrs/ADR-005-audit-driven-ux-a11y-polish.md`
5. `docs/adrs/ADR-008-adr-update-gate-for-major-pushes.md`
6. `docs/adrs/ADR-023-figma-mcp-handoff-jop-tokens.md`

## Redaction policy

To protect IP and narrative integrity, this showcase excludes:
- Case-study copy and project narrative data
- Proprietary or client-identifying details
- Private image assets and source files
- Secrets and environment values

See `docs/redaction-checklist.md` for the publishing checklist.
See `docs/maintenance-workflow.md` for the ongoing curation process.

## Maintenance

This showcase is curated manually from a private working repository.

- New accepted decisions may be copied in as ADRs when safe.
- Snippets are updated only after sanitization.
- Process docs are updated when workflow changes materially.
