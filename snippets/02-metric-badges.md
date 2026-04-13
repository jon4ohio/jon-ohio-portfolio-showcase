# Snippet: Shared Metric Badge Styles

Source pattern: `app/globals.css` (sanitized, non-runnable excerpt).

```css
.metric-badges {
  display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  gap: 6px 8px;
  max-width: 100%;
}

.metric-badge {
  border: 1px solid var(--border);
  border-radius: 999px;
  padding: 3px 8px;
  background: var(--surface);
  display: inline-flex;
  flex-wrap: wrap;
  gap: 3px 5px;
}

.metric-badge__value {
  font-size: clamp(11px, 0.2rem + 2.4vw, 13px);
  font-weight: 700;
}

.metric-badge__label {
  font-size: clamp(9px, 0.15rem + 2vw, 10.5px);
  color: var(--fg-muted);
}
```

Why this matters:
- Uses one shared primitive across multiple pages/components.
- Keeps typography fluid and legible on small screens.
- Reduces drift from copy-pasted inline style objects.
