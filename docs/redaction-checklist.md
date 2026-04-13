# Redaction Checklist

Use this checklist before copying any artifact from the private working repository into this public showcase repository.

## Content safety

- Remove or replace case-study narrative text.
- Replace real project names with placeholders when needed.
- Remove confidential client references.

## Asset safety

- Do not copy private images or source design files.
- Do not include direct links to private asset buckets.
- Use placeholders or synthetic examples instead.

## Technical safety

- Remove API keys, tokens, and environment values.
- Remove internal URLs, webhook endpoints, and tracking parameters.
- Avoid exposing private branch names or internal infrastructure details.

## Snippet safety

- Keep snippets non-runnable and minimal.
- Include only high-signal implementation fragments.
- Remove any embedded product copy or asset paths.

## ADR safety

- Keep decision structure intact.
- Redact sensitive names or references if present.
- Ensure references do not require private repository access to understand the decision.

## Final pass

- Confirm all files are intentional and curated.
- Confirm no accidental secrets or private copy remain.
- Confirm published docs still tell a coherent process story.
