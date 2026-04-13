# Snippet: Responsive Grid Utilities

Source pattern: `app/globals.css` (sanitized, non-runnable excerpt).

```css
/* Desktop defaults */
.grid-4 { display: grid; grid-template-columns: repeat(4, 1fr); }
.grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); }
.grid-2 { display: grid; grid-template-columns: repeat(2, 1fr); }

/* Tablet <= 900px */
@media (max-width: 900px) {
  .grid-4 { grid-template-columns: repeat(2, 1fr); }
  .grid-3 { grid-template-columns: repeat(2, 1fr); }
}

/* Mobile <= 640px */
@media (max-width: 640px) {
  .grid-2 { grid-template-columns: 1fr; }
  .grid-3 { grid-template-columns: 1fr; }
}
```

Why this matters:
- Keeps responsive behavior centralized in one CSS layer.
- Preserves inline-style conventions for decorative properties.
- Demonstrates explicit breakpoint intent instead of implicit utility sprawl.
