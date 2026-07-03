# Motion — Durations, Easing, Choreography

Loaded at Phase 3 (tokens) and applied in Phase 4 (screens). Motion is the part of a design system most often left to chance; here it's tokenized like color.

## 1. Motion has exactly three jobs

1. **Orient** — where did this come from, where did it go (drawer slides from its edge; deleted row collapses toward its list)
2. **Connect** — cause and effect (the button you pressed is the thing that responds)
3. **Confirm** — it worked (state change reads without a toast)

Decorative motion gets **one** signature moment per product (a hero type-on, an ambient mesh, a spring pop) — chosen deliberately in Phase 2, never sprinkled.

## 2. Duration tokens

| Token | Value | Used for |
|---|---|---|
| `--duration-fast` | 100–150ms | hover, toggles, color/opacity shifts |
| `--duration-base` | 200–250ms | dropdowns, tooltips, small reveals |
| `--duration-slow` | 300–400ms | modals, drawers, accordions |
| `--duration-page` | 400–500ms | route/page transitions |

Rules of thumb: smaller distance & smaller element → shorter; **exits ≈ 80% of the paired entrance** (leaving should feel lighter than arriving); nothing exceeds 600ms except the one signature moment; two elements animating together share one duration token, not two similar values.

Calm directions sit at the low end of every range and skip springs; playful directions ride the high end and may overshoot.

## 3. Easing tokens

```css
--ease-out:    cubic-bezier(0.16, 1, 0.3, 1);   /* entrances: fast start, soft settle */
--ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);  /* moves/morphs within the view */
--ease-in:     cubic-bezier(0.5, 0, 0.75, 0);   /* exits only — accelerate away */
```

- Entrances **never** use ease-in (arriving slow reads as lag). Exits never use ease-out (leaving slow reads as clingy).
- Browser-default `ease` everywhere is a slop tell; the custom curves above are the difference between "animated" and "designed."
- **Springs** (playful/toy directions): CSS `linear()` approximation for a light overshoot —
  `--ease-spring: linear(0, 0.3, 0.66, 0.9, 1.03, 1.06, 1.03, 1.005, 0.995, 1)` — or keyframe scale `0.96 → 1.02 → 1`. Springs are for entrances and confirmations, never exits.

## 4. Choreography

- **Stagger** list/grid entrances 20–40ms per item, cap total at ~400ms (12+ items: stagger the first 8, land the rest together).
- **One thing leads.** In a composite transition the primary surface moves first; contents follow with a small delay — everything simultaneously is noise, everything sequential is slow.
- Transform origin matches the trigger: a menu from a top-right button scales from `top right`, not center.
- Hover states: transition `--duration-fast` both directions; transform-based lifts stay subtle (translateY(-1–2px) or scale ≤1.02) with the shadow transitioning in step.

## 5. Performance & respect

- Animate **transform and opacity only** — they run on the compositor. Animating width/height/top/margin causes layout thrash; when a size must animate, use transform-scale + FLIP or `grid-template-rows: 0fr → 1fr` for accordions.
- `will-change` only on elements that actually animate frequently, applied just-in-time.
- **`prefers-reduced-motion` is a requirement, not polish:**

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

plus design intent: movement collapses to opacity crossfades; ambient/looping motion stops entirely; the signature moment gets a static equivalent. State this behavior in the token YAML (`reduced-motion: crossfade`) so implementers inherit the decision.

- Page-level transitions may note the View Transitions API as progressive enhancement — never a dependency.

## 6. Sanctioned patterns

Define 2–3 named patterns in the system; screens use only these:

- **fade-rise** — `opacity 0→1, translateY(8px)→0, --duration-base, --ease-out` (cards, sections, toasts)
- **scale-in** — `opacity 0→1, scale(0.96)→1, --duration-base, --ease-out, origin from trigger` (menus, popovers, modals)
- **slide-panel** — `translateX(100%)→0, --duration-slow, --ease-out; exit reverses with --ease-in at 80% duration` (drawers, sheets)

A screen needing a fourth pattern is a Phase 3 revision (Rule 5), not an improvisation.
