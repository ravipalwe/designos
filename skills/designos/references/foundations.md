# Foundations — Color, Type, Space, Depth

Loaded at Phase 3. This is the craft that turns a direction into a system. Everything here produces exact values; `scripts/color.py` verifies the color ones.

## 1. Color

### Build in OKLCH, ship as hex

OKLCH is perceptually uniform: equal lightness steps *look* equal, and lightness (L) predicts contrast — HSL does neither (HSL yellow at 50% and blue at 50% are wildly different perceived brightnesses). Work in OKLCH, export hex.

**Ramps.** Each color family becomes an 11-step ramp (50–950). Generate with the script, then tune:

```bash
python3 scripts/color.py ramp 250 --chroma 0.13            # brand blue family
python3 scripts/color.py ramp 250 --chroma 0.015           # neutrals tinted with brand hue
python3 scripts/color.py ramp 25  --chroma 0.14 --drift 6  # warm family, hue drifts warmer as it darkens
```

- **Tinted neutrals.** Pure gray next to a warm palette looks dead. Give neutrals 0.005–0.02 chroma of the brand hue. Warm directions: never `#FFFFFF`/`#000000` — paper (`L≈0.97`, warm hue) and ink (`L≈0.22`) instead.
- **Hue drift.** Real pigments shift hue as they darken. A few degrees of drift (warm hues → warmer when dark, blues → deeper) makes ramps feel dyed rather than computed. 4–10° is plenty.
- **Chroma taper.** Chroma must fall toward both ends of the ramp or extremes go neon/muddy. The script tapers automatically; verify the 50 and 950 steps by eye.

### Three-tier token architecture

```
primitive        semantic                  component (optional tier)
blue-600    →    accent              →     button-primary-bg
neutral-50  →    background
neutral-0   →    surface
neutral-100 →    surface-sunken
blue-700    →    accent-hover
neutral-900 →    text-primary
neutral-600 →    text-muted
neutral-200 →    border
```

Rules: components reference semantic, semantic references primitive, screens reference semantic/component only. Semantic minimum set: `background, surface, surface-raised, text-primary, text-muted, text-on-accent, accent, accent-hover, accent-subtle, border, border-strong, focus-ring, danger, danger-subtle, success, success-subtle, warning, warning-subtle`. `*-subtle` = tinted backgrounds for badges/alerts (e.g. danger-subtle = red-50, text stays danger-700 on it).

### Distribution and discipline

- **60-30-10:** ~60% background/surface, ~30% structure (text, borders), ~10% accent. If everything is accent-colored, nothing is.
- **Accent = interactive.** The accent means "you can act here." Decorative accent use dilutes the affordance. Status colors (danger/success/warning) never double as brand accent.
- **State ladder:** hover = one ramp step in the darkening direction (light mode: 600→700; dark mode: brighten instead); active = one more step or scale 0.98; disabled = drop to 40% opacity *or* swap to neutral tokens — never desaturate the token itself.

### Dark mode is a second palette, not a filter

- Base surface `L≈0.16–0.20` with the brand hue at low chroma — never pure `#000` (halation for astigmatic users; crushed elevation range).
- **Elevation = lightness.** Raised surfaces get *lighter* (+0.02–0.04 L per level); shadows are nearly useless on dark. Borders `rgba(255,255,255,0.06–0.12)` carry edge definition.
- Text: `L≈0.93` primary (not pure white — it vibrates), `L≈0.70–0.75` muted.
- Accents: raise L, trim chroma slightly vs light mode — saturated light-mode accents go neon on dark.
- Large fills swap to subtle: a solid accent hero in light mode becomes accent-950-tinted surface in dark.
- Verify every dark pair separately — dark mode needs its own `color.py check` run; symmetric inversion regularly fails APCA.

### Contrast — computed, never asserted

Two systems, both via `scripts/color.py check`:

- **WCAG 2.1** (the legal/compliance standard): ≥4.5:1 body text, ≥3:1 large text (24px+/19px bold+) and UI component boundaries. AAA (7:1) for reading-heavy products.
- **APCA** (perceptual, WCAG 3 trajectory — advisory but better, especially on dark): |Lc| ≥ 90 preferred body · 75 body minimum · 60 large text · 45 headlines ≥36px · 30 absolute floor for any text · 15 non-text minimums.

Design targets: body ≥ 7:1 WCAG when the direction allows; muted text stays ≥ 4.5:1 — muted means quieter, not illegible. Placeholder text is text (≥4.5:1). Disabled elements are exempt but should stay ~3:1 for wayfinding.

## 2. Typography

### Scale

Pick a ratio per density: **1.2 (minor third)** for product UI, **1.25** balanced, **1.333** for marketing/editorial. Generate from 16px body, round to whole px (even preferred). 1.2 example: `12 · 13 · 14 · 16 · 19 · 23 · 28 · 33 · 40 · 48`. Two-ratio scales are legitimate craft: 1.2 below body (UI chrome stays tight), 1.333 above (display gets drama).

Name steps by role, not size: `caption, small, body, body-lg, h3, h2, h1, display`.

### The per-step matrix

Every step defines four values together:

| Role | Size | Weight | Line-height | Letter-spacing |
|---|---|---|---|---|
| display | fluid 40→64 | 650–800 | 1.05–1.1 | −0.02 to −0.04em |
| h1 | 33–40 | 650 | 1.15 | −0.02em |
| h2 | 28 | 600 | 1.2 | −0.01em |
| h3 | 19–23 | 600 | 1.3 | 0 |
| body | 16 | 400 | 1.5–1.6 | 0 |
| small | 14 | 400 | 1.45 | 0 |
| caption/label | 12–13 | 500 | 1.4 | +0.01–0.03em (+0.06–0.12em if uppercase) |

Principles behind the matrix: line-height is inverse to size; tracking tightens as display grows (grotesks especially) and loosens for small/uppercase; **never letterspace lowercase body text**; skip a weight between hierarchy levels (400→600, not 400→500) so hierarchy survives bad rendering.

### Fluid display sizes

`clamp(min, intercept + slope, max)` — slope `= (max−min)/(maxVW−minVW)×100` vw; intercept `= min − slope×minVW/100`.
Example, 32→56px across 400→1280 viewport: `clamp(32px, 21.1px + 2.73vw, 56px)`. Fluid for h1/display only; body stays fixed 16px.

### Craft details

- Measure: 45–75ch body (`max-width: 65ch` on prose), 20–35ch headlines.
- `text-wrap: balance` on headlines, `text-wrap: pretty` on prose. `font-optical-sizing: auto` for opsz faces (Fraunces, Source Serif 4, Newsreader, Bodoni Moda).
- **Data gets `font-variant-numeric: tabular-nums`** — tables, timers, prices, anything that aligns or ticks. Right-align numeric columns.
- Fallback stacks always (`"Fraunces", Georgia, serif` · `"Inter", system-ui, sans-serif` · `"JetBrains Mono", ui-monospace, monospace`). Google Fonts link with `display=swap`, only the weights actually used.
- Never fake bold or italic — load the real weight/style or restructure.
- `-webkit-font-smoothing: antialiased` on dark backgrounds (light-on-dark renders too heavy otherwise); leave default on light.

## 3. Spacing & Layout

### Scale

Base 4. Component range `4 8 12 16 20 24 32`, layout range `40 48 64 80 96 128`. Name by step (`space-1` … `space-32`) or size (`xs…4xl`) — either, consistently. Airy directions live in the upper half; dense directions in the lower — same scale, different diet.

### Proximity is hierarchy

Spacing *encodes relationship*: gap within a group < gap between groups, ratio ≥ 1.5×. A label sits 4–8px from its field and 16–24px from the previous field — get this wrong and no amount of color fixes the grouping. Padding within a container ≤ margin between containers.

### Grid and containers

- Marketing/editorial: 12-column, 24px gutters, max-width 1140–1280px.
- Product UI: regions (sidebar 240–280px, content, optional rail 320–360px) on an 8px soft grid rather than strict columns.
- Prose column: 65–75ch. Full-bleed is a decision, not a default.
- Touch targets: **≥24×24px is the WCAG 2.2 AA floor; design to 44×44 (Apple HIG) / 48 (Material) for primary mobile actions.** Icon buttons get padding to reach target size even when the glyph is 16–20px.

### Optical corrections

Machines center bounding boxes; eyes center visual weight. Play/arrow glyphs nudge 1–2px toward their pointing direction inside circles; icons beside text sit on the text's optical center (usually 1px down from geometric); text baselines align across mixed sizes in a row — align baselines, not boxes. When perfect-by-numbers looks wrong, trust the eye and note the nudge in a comment.

## 4. Radius, Borders, Elevation

### Radius

Scale of 3–4 named steps + `full`, e.g. `sm 4 · md 8 · lg 16 · full 9999`. Radius is brand voice: 0–2 serious/technical · 4–8 neutral product · 12–20 friendly · pills playful. **Concentric rule:** nested radius = outer radius − gap (card 16px with 8px padding → inner element 8px). Matching inner to outer is the most common radius mistake — corners visibly pinch.

### Borders vs shadows — pick a primary depth strategy

Every direction commits: **hairline world** (1px low-contrast borders, shadows rare — editorial, Swiss, industrial), **shadow world** (layered soft shadows, borders rare — humanist, playful), or **lightness world** (dark modes: elevation by surface lightness + subtle borders). Mixing all three per-element is how interfaces get muddy.

### Shadows that don't look stock

Two layers minimum — ambient + key — and **tinted with the surface hue**, never pure black alpha:

```css
--shadow-sm: 0 1px 2px oklch(0.2 0.03 <hue> / 0.06), 0 2px 8px oklch(0.2 0.03 <hue> / 0.05);
--shadow-md: 0 2px 4px oklch(0.2 0.03 <hue> / 0.06), 0 8px 24px oklch(0.2 0.03 <hue> / 0.08);
--shadow-lg: 0 4px 8px oklch(0.2 0.03 <hue> / 0.08), 0 16px 48px oklch(0.2 0.03 <hue> / 0.12);
```

Larger blur = lower opacity. Hard-offset shadows (brutalist) are the exception: solid, no blur, and that *is* the signature.

### Focus is designed, not default

`:focus-visible` gets a deliberate ring: `outline: 2px solid var(--focus-ring); outline-offset: 2px` (offset −2px/inset on filled buttons). The focus-ring token needs 3:1 against adjacent colors. Never `outline: none` without a visible replacement — this is a hard accessibility failure.

## 5. Token YAML schema (for `03-design-system.md`)

```yaml
meta:        {product, direction, signature, date}
color:
  primitives: {neutral: {0:"#…", 50:"#…", …, 950:"#…"}, <family>: {…}}
  semantic:
    light: {background:"#…", surface:"#…", surface-raised:"#…", text-primary:"#…",
            text-muted:"#…", text-on-accent:"#…", accent:"#…", accent-hover:"#…",
            accent-subtle:"#…", border:"#…", border-strong:"#…", focus-ring:"#…",
            danger:"#…", danger-subtle:"#…", success:"#…", success-subtle:"#…",
            warning:"#…", warning-subtle:"#…"}
    dark:  {…same keys…}          # only if dark mode in scope
  verified: "color.py check — all pairs pass; see Contrast table"
type:
  families: {display: {name, fallback, weights}, body: {…}, mono: {…}}
  scale:    {display: {size|clamp, weight, line, tracking}, h1: {…}, h2: {…},
             h3: {…}, body: {…}, small: {…}, caption: {…}}
space:     {base: 4, steps: [4,8,12,16,20,24,32,40,48,64,80,96,128]}
radius:    {sm: 4, md: 8, lg: 16, full: 9999}
shadow:    {sm: "…", md: "…", lg: "…"}    # or borders: {…} per depth strategy
motion:    {duration: {fast: 120ms, base: 200ms, slow: 300ms, page: 450ms},
            easing: {out: "cubic-bezier(0.16,1,0.3,1)", in-out: "cubic-bezier(0.65,0,0.35,1)"},
            stagger: 30ms, reduced-motion: "crossfade"}
breakpoints: {sm: 640, md: 900, lg: 1200}   # only what the platform needs
components:  # per component: tokens consumed + state notes
  button-primary: {bg: accent, text: text-on-accent, hover: accent-hover,
                   radius: md, height: 40, states: [default,hover,active,focus-visible,disabled]}
  …
```

After the YAML block, prose rationale per section — *why this ratio, why this hue strategy, why this depth model* — two to five sentences each. The rationale is what lets a future session (or another designer) extend the system instead of breaking it.

## 6. The style guide (`03-design-system.html`)

- Designed **in the system it documents** — the guide itself is the first implementation and the first test.
- Sections: identity header (direction name, signature, principles) → color (swatch grid, each labeled hex + WCAG ratio + APCA Lc from the script) → type scale (rendered, with the matrix values) → spacing bars → radius/shadow specimens → every component in every state (real labels, not "Button") → motion specimens (hover a card to feel `--duration-base`).
- Dark-mode toggle if dark exists (swap a `data-theme` attribute; tokens defined for both).
- All tokens as CSS custom properties in one `:root` block — this block is what Phase 4 screens copy verbatim.
