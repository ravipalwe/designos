# Solvent Design System — Paper Ledger

Source of truth. The mirror for humans is `03-design-system.html`. Every color pair below was verified with `scripts/color.py` (WCAG 2.1 gate + APCA advisory) — the Contrast table at the end is the receipt.

```yaml
meta:
  product: Solvent
  direction: Paper Ledger
  signature: Ledger hairlines — every number sits on ruled paper
  date: 2026-07-02

color:
  primitives:
    neutral:   # OKLCH hue 78 (the ink's own hue), chroma 0.012 — warm, never dead gray
      50: "#F8F6F3"
      100: "#E0DDD8"
      200: "#C7C3BE"
      300: "#AFABA5"
      400: "#98938C"
      500: "#807C75"
      600: "#6A655F"
      700: "#54504A"
      800: "#3E3B37"
      900: "#2A2825"
      950: "#171614"
    oxide:     # OKLCH hue 35, drift +4 toward warmth as it darkens
      50: "#FFF2EF"
      100: "#FFD0C6"
      200: "#FEAC9B"
      300: "#ED907B"
      400: "#DA745D"
      500: "#C35B41"
      600: "#A7472E"
      700: "#89371F"
      800: "#6A2814"
      900: "#4C1B0C"
      950: "#2F1006"
    brand:
      paper: "#FAF7F2"     # oklch(0.977 0.007 81) — the page
      ink: "#1C1A17"       # oklch(0.219 0.007 78) — the pen
      oxide: "#C24A2C"     # oklch(0.567 0.160 35) — tuned between oxide-500/600
      rule: "#E4DED2"      # the hairline
    status:
      success: "#3C784B"
      success-subtle: "#E4F2E7"
      success-text: "#2E5D3A"
      danger: "#AB4042"
      danger-subtle: "#FDEEED"
      danger-text: "#8B3134"
      warning: "#846308"
      warning-subtle: "#F7EFDC"
      warning-text: "#6B5006"
  semantic:
    light:
      background: "#FAF7F2"        # brand.paper
      surface: "#FFFFFF"
      surface-sunken: "#F8F6F3"    # neutral-50
      text-primary: "#1C1A17"      # brand.ink
      text-muted: "#67625D"        # tuned warm neutral, AA on paper AND surface
      text-on-accent: "#FFFFFF"
      accent: "#C24A2C"            # brand.oxide
      accent-hover: "#A7472E"      # oxide-600
      accent-subtle: "#FFF2EF"     # oxide-50
      accent-text-on-subtle: "#89371F"  # oxide-700
      border: "#E4DED2"            # brand.rule — THE hairline
      border-strong: "#C7C3BE"     # neutral-200
      focus-ring: "#C24A2C"
      danger: "#AB4042"
      danger-subtle: "#FDEEED"
      success: "#3C784B"
      success-subtle: "#E4F2E7"
      warning: "#846308"
      warning-subtle: "#F7EFDC"
    dark: null   # out of scope v1 — see 02-direction.md Consequences
  verified: "color.py check 2026-07-02 — 14/14 pairs PASS; table below"

type:
  families:
    display: {name: Fraunces, fallback: "Georgia, serif", weights: [600], features: "font-optical-sizing: auto"}
    body:    {name: Figtree, fallback: "system-ui, sans-serif", weights: [400, 500, 600]}
  scale:     # ratio 1.2 below display; display goes fluid
    display: {size: "clamp(40px, 26.9px + 1.64vw, 56px)", weight: 600, line: 1.08, tracking: "-0.015em", family: display}
    h1:      {size: 33, weight: 600, line: 1.15, tracking: "-0.01em", family: display}
    h2:      {size: 28, weight: 600, line: 1.2, tracking: "-0.005em", family: display}
    h3:      {size: 19, weight: 600, line: 1.3, tracking: "0", family: body}
    body:    {size: 16, weight: 400, line: 1.55, tracking: "0", family: body}
    small:   {size: 14, weight: 400, line: 1.45, tracking: "0", family: body}
    caption: {size: 12, weight: 500, line: 1.4, tracking: "+0.02em", family: body}
    label:   {size: 11, weight: 600, line: 1.3, tracking: "+0.09em", family: body, transform: uppercase, color: text-muted}
    amount:  {size: inherit, weight: 500, family: body, features: "font-variant-numeric: tabular-nums"}
  rules:
    - "Amounts and dates always .amount (tabular) — principle 3"
    - "Fraunces only ≥19px; UI chrome is Figtree"
    - "text-wrap: balance on headings"

space: {base: 4, steps: [4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 96]}

radius: {sm: 2, md: 4, full: 9999}   # ledger world: nothing rounder than 4

depth:
  strategy: hairline   # borders carry structure; shadows are for the one floating layer
  border: "1px solid var(--color-border)"
  shadow-modal: "0 2px 4px oklch(0.2 0.02 78 / 0.05), 0 12px 32px oklch(0.2 0.02 78 / 0.10)"

motion:
  duration: {fast: 120ms, base: 200ms, slow: 320ms, page: 450ms}
  easing:
    out: "cubic-bezier(0.16, 1, 0.3, 1)"
    in-out: "cubic-bezier(0.65, 0, 0.35, 1)"
    in: "cubic-bezier(0.5, 0, 0.75, 0)"
  stagger: 30ms
  patterns: [fade-rise, scale-in, slide-panel]
  reduced-motion: crossfade
  character: "page-like — fades and small vertical settles; nothing bounces"

breakpoints: {sm: 640, lg: 1024}

components:
  button-primary:    {bg: accent, text: text-on-accent, hover-bg: accent-hover, radius: md, height: 40, pad-x: 18, type: "600 14px body"}
  button-secondary:  {bg: surface, text: text-primary, border: border-strong, hover-border: text-muted, radius: md, height: 40}
  button-ghost:      {bg: transparent, text: text-muted, hover-text: text-primary, hover-bg: surface-sunken, radius: md, height: 36}
  button-destructive:{bg: danger, text: text-on-accent, radius: md, height: 40, note: "destructive only — principle 2"}
  input:             {bg: surface, border-bottom: "1px solid border-strong", focus-border: accent, radius: 0, height: 40,
                      note: "underline fields — form rows ARE ledger lines (signature)"}
  field-error:       {text: danger-text, size: caption, icon: "required — never color alone"}
  card:              {bg: surface, border: border, radius: md, pad: 24}
  ledger-row:        {height: 44, border-bottom: border, cols: "payee | date muted | amount right tabular"}
  badge:             {bg: "*-subtle", text: "*-text", radius: sm, pad: "2px 8px", type: caption}
  nav:               {bg: background, border-bottom: border, height: 56, wordmark: "Fraunces 600 19px"}
  modal:             {bg: surface, border: border, radius: md, shadow: shadow-modal, backdrop: "oklch(0.22 0.007 78 / 0.4)"}
  toast:             {bg: ink, text: paper, radius: md, motion: fade-rise}
  empty-state:       {icon: "hairline ruled lines motif", title: h3, body: "small muted", action: button-primary}
  focus-ring:        {style: "outline: 2px solid focus-ring; outline-offset: 2px", inset-on-filled: true}
  states: [default, hover, active, focus-visible, disabled]   # all interactive components, all five
```

## Rationale

**Color.** Neutrals are the ink's own OKLCH hue (78°) at 0.012 chroma — the whole page feels dyed in one warm bath, never dead gray. The oxide ramp drifts +4° warmer as it darkens, so hover states deepen like fired clay instead of going muddy. Per principle 2, status colors are rationed: negative amounts are ink (a kept book, not an alarm panel); danger exists for destructive actions only. `text-muted` was tuned to `#67625D` — it passes AA on *both* paper and white surfaces, so one token serves every context.

**Type.** Fraunces (optical sizing on) gives numbers the gravity of set type; Figtree stays invisible in the chrome. Ratio 1.2 keeps a product-UI temperament — drama comes from the display step going fluid, not from wide jumps. The `amount` style is a first-class type token because tabular figures are principle 3 in CSS form.

**Space & depth.** 4-base scale; the ledger's density lives in the 12–24 range with 48–96 between regions. Depth strategy is hairline: `--color-border` does the work shadows would, which keeps the page flat like paper. Exactly one shadow exists (modals) because a modal genuinely floats.

**Motion.** Page-like: fade-rise and scale-in at 200ms with a decisive ease-out. Nothing bounces — calm 5. Exits run 80% duration with ease-in. Reduced motion collapses everything to crossfades.

## Contrast receipt (color.py, 2026-07-02)

| pair | ratio | grade | APCA |
|---|---|---|---|
| text-primary / background | 16.25:1 | AAA | +99.6 |
| text-muted / background | 5.64:1 | AA | +75.6 |
| text-primary / surface | 17.36:1 | AAA | +104.2 |
| text-muted / surface | 6.03:1 | AA | +80.2 |
| text-on-accent / accent | 4.87:1 | AA | −78.4 |
| text-on-accent / accent-hover | 5.86:1 | AA | −83.9 |
| accent as large text / background | 4.56:1 | AA | +68.3 |
| accent-text-on-subtle / accent-subtle | 7.30:1 | AAA | +80.8 |
| success ui / background | 4.94:1 | AA | +71.4 |
| success-text / success-subtle | 6.62:1 | AA | +76.5 |
| danger ui / background | 5.55:1 | AA | +74.3 |
| danger-text / danger-subtle | 7.20:1 | AAA | +79.1 |
| warning ui / background | 5.21:1 | AA | +73.0 |
| warning-text / warning-subtle | 6.61:1 | AA | +76.9 |
