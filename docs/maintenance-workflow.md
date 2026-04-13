# Maintenance Workflow

This repository is a curated mirror of process artifacts from a private working repository.

## When to update

Update the public showcase when a meaningful decision or implementation pattern is complete and safe to disclose.

## Update steps

1. Select the artifact to publish (ADR and/or snippet).
2. Run the redaction checklist in `docs/redaction-checklist.md`.
3. Copy and sanitize content into `docs/adrs/` or `snippets/`.
4. Update `docs/adrs/index.md` if ADR coverage changes.
5. Update `README.md` receipts links if new files were added.

## Publishing rules

- Publish high-signal evidence, not bulk code.
- Keep snippets non-runnable and content-free.
- Do not publish case-study narrative data or private assets.
- Prefer small, clear updates over large dumps.

## Review cadence

- Quick review: each time a new artifact is added.
- Full repository hygiene review: monthly.
