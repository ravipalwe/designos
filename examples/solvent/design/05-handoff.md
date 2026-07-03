# Solvent — Implementation Handoff

For the implementing agent or engineer. Everything you need is in this folder; nothing outside it is designed. Read this file top to bottom (5 minutes), then follow the build order.

## 1. Token export

Paste the `:root` block from `03-design-system.html` (lines under `/* ============ TOKENS`) into the global stylesheet **verbatim — do not edit token values**. It includes the `prefers-reduced-motion` block; keep it. Stack was not detected (design-only example); if the implementation uses Tailwind v4, map the same custom properties in an `@theme` block using semantic names (`--color-accent`, not raw hexes).

Contrast is already verified (receipt in `03-design-system.md`). If you introduce any **new** color pair, run:
`python3 <designos>/scripts/color.py check "FG BG label"` — it must pass before shipping.

## 2. Build order

### 0 · Foundations
- [ ] Global styles: token block, Google Fonts (Fraunces 600 opsz + Figtree 400/500/600, `display=swap`), reset, `:focus-visible` ring, reduced-motion
- [ ] `.amount` utility — `font-variant-numeric: tabular-nums; font-weight: 500` (**QA check: confirm Figtree renders true tabular figures in your target browsers; if columns wobble, substitute the numerals' font-feature or file an issue — do not drop the requirement**)
### 1 · Primitives (specs + all five states in `03-design-system.html`)
- [ ] Button: primary / secondary / ghost / destructive
- [ ] Field: underline input + label + hint + error (error icon+text, never color alone)
- [ ] Ledger row · Badge (4 tints) · Toast · Card · Empty state
### 2 · Composites
- [ ] Nav (top bar, active = 2px accent underline)
- [ ] Ledger table (compact: 40px rows, month groups, right-aligned amounts)
- [ ] Unsaved-changes bar (fixed bottom, ink bg, fade-rise)
### 3 · Screens (priority order — mockup is the spec)
- [ ] `dashboard.html` — states: default, empty
- [ ] `transactions.html` — states: default, row badges, truncation
- [ ] `assumptions.html` — states: default, field error, unsaved bar
### 4 · Design QA (per screen, §4)

## 3. Per-screen notes

**dashboard** — Data: current runway (months, 1 decimal), solvent-until date, balance series (6 mo), month stats (burn/income/net + comparators), latest 7 ledger entries. Behavior: runway recomputes on every ledger change; sparkline is decorative (no tooltips v1); "Add transaction" opens a modal (scale-in pattern, `shadow-modal`) — modal itself reuses the assumptions field primitives. Empty state replaces the entire main region when entry count = 0.

**transactions** — Data: paginated entries (50/page, infinite scroll), month grouping by posted date. Behavior: search filters payee live (debounce ~200ms); chips are exclusive filters; failed-sync rows show Retry inline; amounts column right-aligned tabular always. Mobile: category column drops (already in mockup's media query).

**assumptions** — Behavior: preview recomputes on input (the mockup's JS is the reference math: `months = (cash − oneoffs) / (burn − income)`, ∞ → "Default alive"); invalid input shows the field error and freezes the preview at last valid state; unsaved bar appears on first divergence, Discard restores observed values. Save persists overrides and re-runs the dashboard recompute.

## 4. Acceptance criteria (every screen)

- [ ] Every color/space/type value traces to a token — no magic numbers in the diff
- [ ] All five interactive states work; `:focus-visible` ring on every focusable element; tab order = visual order
- [ ] Screen states from the mockup implemented (state dividers in mockups mark them)
- [ ] Targets ≥24px (44px for primary mobile actions); headings sequential; reduced-motion honored
- [ ] 375px and 1024px+ both genuinely usable
- [ ] **Screenshot the built screen at both widths and compare side-by-side with the mockup.** Drift → fix the code. Something the mockup couldn't know → record it below under QA deltas. The mockups stay the source of truth.

## QA deltas
_(record intentional divergences here during implementation — date + one line each)_

## 5. Out of scope — do not improvise

Not designed in v1: **dark mode** (decided at direction gate — see `02-direction.md`) · auth/onboarding beyond the empty state · settings & billing · mobile bottom-nav (top nav persists at all widths in v1) · charts beyond the sparkline · email templates · marketing site.

When any of these becomes needed: **stop and run DesignOS** (Resume mode — `design/STATE.md` holds full context). Don't invent inside the codebase.

## Quick start

1. Read this file top to bottom.
2. Paste the token block. Do not edit token values.
3. Follow the build order; check items off in this file.
4. Screenshot-QA each screen against its mockup before marking done.
5. Unclear or undesigned? Run DesignOS — don't invent.
