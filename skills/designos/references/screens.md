# Screens — Content-First Design & the Mockup Craft Bar

Loaded at Phase 4. A screen mockup from DesignOS should feel eerily like the shipped product — real words, real data shapes, real states, real keyboard behavior. This file defines the method and the quality bar.

## 1. Content before layout

Layout arranges content; without content it arranges guesses. Before any HTML, write the screen's actual words in the product's voice:

- **Headline / page title** — what the user came for, not the feature's internal name ("Your runway" beats "Financial Dashboard")
- **Primary action label** — a verb phrase: "Create invoice", "Invite teammate". Never "Submit", "OK", "New".
- **Empty state** — first-run is a pitch: one line of value + the primary action. Not "No data yet."
- **Error messages** — what happened + how to recover, in one breath ("Card declined — try another card or check with your bank"). Never blame, never bare codes.
- **Microcopy defaults** — sentence case everywhere (unless the direction argues otherwise, e.g. industrial small-caps labels); numbers formatted (`1,204` not `1204`, currency with cents); dates as the user thinks (`Today, 4:12 PM`, `Mar 14`).

Write these into the screen's spec block in `index.md`, then build.

## 2. Hierarchy

- **One primary action per screen.** One filled accent button; everything else secondary/ghost. Two filled buttons = no decision was made.
- **The 5-second test:** name of screen, what it's for, what to do next — all readable at a glance. If not, the hierarchy is lying somewhere.
- Visual weight budget: size → weight → color → position, in that order of preference. Reach for color last; it's the loudest and cheapest lever.
- Reading gravity: F-pattern for dense/data screens, Z-pattern for sparse/marketing. Put the decision where the eye exits.

## 3. Real data rules

Realistic data is design material — it stress-tests the layout:

- **Vary lengths deliberately:** one short name ("Ada Chen"), one long ("Konstantinos Papadopoulos-Wright"), one that truncates — the truncation *is* the test. Same for titles, emails, amounts.
- Numbers with texture: `$12,847.50`, `−$320.11`, `$0.00`, `99+`. Round numbers everywhere read as fake.
- Names/emails from varied cultures; no "John Doe", no `user@example.com`, no `Jane Smith`.
- Dates mixed as the product would show them: relative for recent (`2h ago`), absolute past that (`Mar 14, 2026`).
- Every list shows a realistic count — 7 items, not 3 perfect ones. Include one item in a non-default state (overdue, syncing, archived) so the state design is visible.
- Imagery: design the treatment (aspect ratio, radius, overlay, alt-pattern like initials-on-tinted-background) — never a gray placeholder box.

## 4. States are the screen

A screen isn't designed until its states are. For each screen decide which of these are *the point* and include them in the mockup (tabs or stacked sections labeled clearly):

- **Empty** (first-run) — value + action, possibly illustration/diagram per direction
- **Loading** — skeletons that match the final layout exactly (no shift on arrival); show nothing under ~300ms rather than flashing
- **Partial** — 1 item; and the implied 999-item case (what scrolls, what truncates, what paginates)
- **Error** — inline recovery, not a dead end
- **Success/confirmation** — often just motion + a subtle change; toast only when the change happens out of view

Interactive states come free with the system (hover/active/focus from Phase 3) but must be *wired* in the mockup: real `:hover`, real `:focus-visible`, disabled attributes where relevant.

## 5. Density

- Marketing/editorial: airy — body 16–18px, sections 96–128px apart, measure ≤72ch.
- Product default: comfortable — 44–48px rows, 16px body, 24px card padding.
- Data-heavy: compact earns its keep — 32–36px rows, 13–14px `tabular-nums`, 8–12px cell padding, hairline row separators, headers as small-caps labels. Right-align numbers, left-align text, never center either.
- Pick per screen from the direction's home range; note it in the spec block.

## 6. Responsive

- Breakpoints come from the system (Phase 3); the mockup must be genuinely usable at 375px and at the design width — test both before presenting.
- Mobile is not "desktop, squeezed": navigation collapses deliberately (bottom bar / sheet — decide which), tables become cards or column-pruned lists (decide which columns survive), touch targets hit 44px, hover-revealed actions get a visible mobile affordance.
- Use CSS grid/flex with `minmax()`/`clamp()` so layouts flex between breakpoints rather than jump. Container queries where a component (card, row) must adapt to its region rather than the viewport.

## 7. The mockup craft bar (`04-screens/<screen>.html`)

Every screen file meets all of this:

1. **Self-contained** — tokens pasted as the `:root` block from `03-design-system.html`, verbatim. Google Fonts link + fallbacks. No other externals.
2. **Semantic HTML** — `header/nav/main/aside/section/button/table` doing their jobs; `aria-label` where structure alone is ambiguous; heading levels sequential. A screen reader should make sense of the mockup — this is the cheapest possible a11y head start for implementation.
3. **Keyboard-real** — tab order follows visual order; `:focus-visible` rings visible on every interactive element; nothing interactive is a bare `div`.
4. **Wired states** — hovers transition with motion tokens; the screen's key states present per §4.
5. **Dev overlay** — include this standard snippet at the end of `<body>`; it's DesignOS's field kit:

```html
<div id="dx" hidden></div>
<style>
  #dx { position: fixed; inset: 0; pointer-events: none; z-index: 9999;
    background:
      repeating-linear-gradient(to bottom, transparent 0 7px, oklch(0.6 0.2 20 / 0.12) 7px 8px),
      repeating-linear-gradient(to right, transparent 0 7px, oklch(0.6 0.2 20 / 0.08) 7px 8px); }
  body.blur-test > *:not(#dx) { filter: blur(6px); }
</style>
<script>
  addEventListener('keydown', e => {
    if (e.target.matches('input,textarea,select')) return;
    if (e.key === 'g') dx.hidden = !dx.hidden;                 // 8px grid overlay
    if (e.key === 'b') document.body.classList.toggle('blur-test'); // squint test
  });
</script>
```

`g` toggles the 8px grid (spacing honesty), `b` blurs the page (hierarchy honesty — the squint test, live). Mention the shortcuts once when presenting the first screen.

6. **Crit passed** — the full protocol from `critique.md`, including the slop scan and signature check, before the user ever sees it.

## 8. Screen spec block (in `04-screens/index.md`)

```markdown
## <n>. <screen-name>  — <status: specced | built | approved>
Purpose: <one line — the job this screen does>
Effortless thing: <the single interaction this screen optimizes>
Layout: <skeleton in one line, e.g. "sidebar 260 / content 720 / rail 340">
Density: <airy | comfortable | compact>
States in mockup: <default, empty, …>
Microcopy: headline "<…>" · primary "<…>" · empty "<…>" · error "<…>"
```
