# Handoff — Token Export, Build Order, Design-QA

Loaded at Phase 5. The handoff's job: an implementing agent (or engineer) ships the design *without asking questions and without inventing anything*. Everything below lands in `design/05-handoff.md`.

## 1. Token export

Pick the format(s) the stack detected in Phase 0 actually uses. Always include the CSS custom-property export; add the others when they apply.

### CSS custom properties (universal)

One `:root` block, grouped and commented. Both modes via `light-dark()` with a `color-scheme` declaration; fall back to a `data-theme` attribute swap if the product needs manual toggling:

```css
:root {
  color-scheme: light dark;
  /* color — semantic */
  --color-background: light-dark(#FAF7F2, #131211);
  --color-surface:    light-dark(#FFFFFF, #1B1A18);
  --color-text:       light-dark(#1C1A17, #EDEBE7);
  --color-accent:     light-dark(#C24A2C, #E07A5A);
  /* type */
  --font-display: "Fraunces", Georgia, serif;
  --font-body: "Figtree", system-ui, sans-serif;
  --text-h1: 600 clamp(32px, 21.1px + 2.73vw, 56px)/1.15 var(--font-display);
  /* space / radius / shadow / motion … every token, no omissions */
}
```

Include the `prefers-reduced-motion` block from the system verbatim. This export must be complete enough that deleting every other style source still leaves the design system intact.

### Tailwind (when the stack uses it)

Tailwind v4: a ready-to-paste `@theme` block mapping tokens to Tailwind names (`--color-accent`, `--font-display`, `--radius-md`, custom `--text-*` sizes). Tailwind v3: `theme.extend` object for `tailwind.config`. Map semantic names, not primitives — implementers should type `bg-surface`, not `bg-neutral-50`.

### DTCG JSON (when a token pipeline / Figma sync exists)

W3C Design Tokens format — `{"color": {"accent": {"$value": "#C24A2C", "$type": "color"}}}` — primitives and semantic as separate groups, semantic referencing primitives with `{color.primitive.oxide.600}` aliases.

## 2. Build order

Dependency-ordered checklist; each item names its source artifact:

```markdown
### 0. Foundations
- [ ] Global styles: tokens block, font loading, reset, focus-visible, reduced-motion (03-design-system.md)
### 1. Primitives (each: all five states, per 03-design-system.html)
- [ ] Button (primary/secondary/ghost/destructive)  - [ ] Input + label + error
- [ ] Card  - [ ] Badge/tag  - [ ] Toast  - [ ] Table row  - [ ] Empty state
### 2. Composites
- [ ] Nav/sidebar  - [ ] Modal/drawer (scale-in / slide-panel patterns)  - [ ] Data table
### 3. Screens — priority order from 04-screens/index.md
- [ ] <screen> (04-screens/<screen>.html) — states: <list>
### 4. Design QA (per screen, §4 below)
```

## 3. Per-screen implementation notes

For each screen: **data requirements** (entities, fields, realistic volumes — "list paginates at 50; truncation at 240px column width"); **behavior the mockup can't show** (sort/filter logic, optimistic updates, keyboard shortcuts, what the primary action *does*); **variants used** (which button/card/row recipes appear, by token name); **responsive deltas** (what collapses, which columns survive mobile, where the nav goes).

## 4. Acceptance criteria & Design-QA loop

Acceptance criteria per screen — the crit protocol converted to QA:

- [ ] Every color/space/type value traces to a token (no magic numbers in review diff)
- [ ] Contrast pairs pass (re-run `scripts/color.py check` on any *new* pair introduced)
- [ ] All five interactive states work; focus-visible ring on every focusable element; tab order = visual order
- [ ] Screen states implemented: <the list from the mockup>
- [ ] Targets ≥24px (44px primary mobile); reduced-motion honored; headings sequential
- [ ] 375px and desktop widths both genuinely usable

**Design-QA loop** (instruct the implementing agent explicitly): after building each screen, screenshot it at the mockup's widths and compare against `04-screens/<screen>.html` side by side. Differences are either (a) implementation drift → fix the code, or (b) something the mockup couldn't know → note it in `05-handoff.md` under "QA deltas" so the design record stays true. Don't let the two silently diverge — the mockups remain the design source of truth after handoff.

## 5. Out of scope — the anti-invention clause

List explicitly what was *not* designed (admin screens, marketing pages, email templates, print, native-app chrome…) with the instruction: **do not improvise these**. When an undesign̈ed surface becomes needed, the implementer returns to DesignOS (Resume mode) so it's designed inside the system. One sentence in this section saves a week of drift.

## 6. Closing block

End `05-handoff.md` with:

```markdown
## Quick start (for the implementing agent)
1. Read this file top to bottom (5 min).
2. Paste the token block into the global stylesheet. Do not edit token values.
3. Follow Build Order. Check items off in this file as you go.
4. Screenshot-QA each screen against its mockup before marking done.
5. Anything unclear or undesigned: stop and run DesignOS (design/STATE.md has full context) — don't invent.
```

Then close the chat with the 5-line system summary and the single next action.
