# The Crit Protocol — Self-Review Before Every Gate

Read once per session; apply before *presenting anything*. The order is deliberate: structure first, polish last, so fixes don't get overwritten by later fixes. Fix everything found, then present — and tell the user in one or two lines what the crit caught ("crit pass tightened muted-text contrast and re-aligned the rail to the 8px grid"). Transparency is part of the craft.

If browser/preview tooling is available in the session, render the HTML and screenshot it — run these passes on the *pixels*, not just the code. Code review catches token discipline; only looking catches a lopsided layout.

## The ten passes

### 1. Squint test (hierarchy)
Blur it — mentally, via screenshot, or the mockup's `b` toggle. Does the primary action still pop? Do groups read as groups? Is there exactly one "loudest" thing? If everything is prominent, nothing is.

### 2. Contrast audit (verified)
Every text/background pair through `scripts/color.py check` — including muted text, placeholders, text on accent, on tinted `*-subtle` surfaces, and every dark-mode pair separately. No asserting; run it.

### 3. Alignment walk
Trace every edge: each one aligns to the grid, a sibling, or a container line. Count distinct vertical alignment lines — fewer is calmer; each extra line needs a reason. Check optical alignment where boxes lie (icons beside text, glyphs in circles).

### 4. Rhythm check (spacing)
Every gap is a scale value — no 13px orphans (`g` overlay verifies). Proximity encodes relationship: within-group < between-group at ≥1.5×. Padding-inside ≤ margin-outside. One-off spacing that "looked right" gets justified or normalized.

### 5. Consistency sweep
Same thing, same look, everywhere: one primary-button recipe, one card recipe, one focus ring. Different things look *deliberately* different — a danger action shouldn't dress like a safe one. Cross-check against `03-design-system.md`, both directions (drifted screen, or a system gap?).

### 6. Content honesty
No lorem, no John Doe, no gray boxes, no invented trust signals, no perfectly round numbers. Lengths vary; one truncation case exists; empty/error copy is written in product voice. Words are design — read them aloud once.

### 7. State completeness
Interactive elements: default/hover/active/focus-visible/disabled, wired not just specced. Screen: the states that are its point (per screens.md §4) are present. Focus rings visible on *every* focusable element — tab through the mockup.

### 8. Slop scan
Run the anti-slop list (direction.md §4). Any hit is deliberate and defensible, or it goes. Then the harder question: *does this look like it was designed by someone, for this product?* If the product name could be swapped for any startup and nothing would feel off, the design hasn't landed yet.

### 9. Signature & principles check
The signature element (STATE.md) is present and undiluted — one signature, quiet everything else. Test each minted principle against the artifact: would this screen survive "Numbers are the interface"? Principles that never get to veto anything are decoration.

### 10. Accessibility pass
Beyond contrast (pass 2): heading levels sequential; semantic elements doing their jobs; tab order follows visual order; touch targets ≥24px minimum, 44px for primary mobile actions; motion has reduced-motion behavior; nothing conveyed by color alone (status = icon/label + color); form fields have real labels, not placeholder-as-label.

## Scaled application

| Artifact | Passes |
|---|---|
| Direction demo (Phase 2) | 1, 2, 6, 8, 9 |
| Style guide (Phase 3) | all ten |
| Each screen (Phase 4) | all ten |
| Handoff doc (Phase 5) | 2 (final full-pair sweep), 5, 7 as checklist audit |

## Receiving human feedback at gates

- Vague reaction ("feels off") → diagnose with the passes: usually hierarchy (1), rhythm (4), or consistency (5). Ask *where* their eye goes first — compare with where it should go.
- Directional adjustments ("warmer", "denser", "calmer") → translate to axis moves and name the concrete change ("warmer → neutrals take hue 60 tint, shadows warm up, paper bg" ), confirm, apply at the token layer.
- Feedback contradicting a minted principle → surface it: "That trades against 'Calm until money moves' — change the principle, or find a calmer route to the same goal?" Principles exist for exactly this moment.
- Feedback that would break another screen → apply at the layer that owns it (Rule 5), regenerate affected artifacts, log the decision.
