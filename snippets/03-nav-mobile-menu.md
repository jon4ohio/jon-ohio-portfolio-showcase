# Snippet: Mobile Nav Toggle Pattern

Source pattern: `components/Nav.tsx` + `app/globals.css` (sanitized, non-runnable excerpt).

```tsx
const [menuOpen, setMenuOpen] = useState(false);

<button
  className="nav-hamburger"
  onClick={() => setMenuOpen(!menuOpen)}
  aria-label={menuOpen ? "Close menu" : "Open menu"}
  aria-expanded={menuOpen}
  aria-controls="nav-mobile-panel"
>
  {/* icon bars omitted */}
</button>

<div
  id="nav-mobile-panel"
  className={`nav-mobile-panel${menuOpen ? " open" : ""}`}
  aria-hidden={!menuOpen}
>
  {/* links omitted */}
</div>
```

```css
.nav-mobile-panel {
  opacity: 0;
  transform: translateY(-8px);
  visibility: hidden;
  pointer-events: none;
  transition: opacity 0.18s ease, transform 0.18s ease, visibility 0.18s ease;
}

.nav-mobile-panel.open {
  opacity: 1;
  transform: translateY(0);
  visibility: visible;
  pointer-events: auto;
}
```

Why this matters:
- Uses explicit accessibility state (`aria-expanded`, `aria-controls`, `aria-hidden`).
- Keeps mobile behavior self-contained and reversible.
- Shows interaction polish without exposing private content.
