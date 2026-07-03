# Direction — Taste, Style Worlds, Distinctiveness

Loaded at Phase 2. This file is the skill's taste. Its job: make the chosen direction *ownable* — something a user could describe in one sentence after closing the tab — and keep it out of the generated-design median.

## 1. Reading the taste profile

The five axes from the brief map to concrete levers:

| Axis | Low end pulls toward | High end pulls toward |
|---|---|---|
| warm↔cool | paper tones, terracotta, serifs, soft shadows | blue-greys, steel, grotesks, hard edges |
| minimal↔expressive | few colors, type-driven, whitespace | display type, illustration, color blocking |
| calm↔energetic | low chroma, slow motion, muted states | high chroma, springs, bold hovers |
| classic↔futuristic | serifs, symmetry, ivory/ink | mono/grotesk, asymmetry, dark surfaces, glow |
| airy↔dense | large type, 96px sections, generous line-height | 13px data type, tight tables, hairline rules |

Directions should *disagree* with each other on at least two axes. Three variations of the same corner is a fake choice.

## 2. Style worlds

Twelve coherent aesthetics with real recipes. Use them as starting points or hybridize ("Editorial structure, Terminal color"). Every typeface listed is on Google Fonts. Seed hexes are starting DNA, not final tokens — Phase 3 rebuilds them as OKLCH ramps.

### Swiss / International
Typography IS the design. Strict grid, flush-left, no decoration.
- Type: Inter Tight (600–800, tight tracking) or Archivo; body Inter/Archivo 400
- Seeds: `#FFFFFF` bg · `#111111` ink · `#E63946` one red accent · `#F2F2F0` surface · `#6D6D6D` muted
- Shape: radius 0–2px, 1px rules, **no shadows** — hierarchy from scale and weight alone
- Motion: instant and precise, 150ms, no bounce
- Fits: portfolios, publications, agencies, anything wanting authority
- Risk: sterile if content is thin — needs strong type scale jumps (1.333+)

### Editorial / Magazine
Reads like a well-set publication: serif display, generous measure, hairlines.
- Type: Fraunces (display, opsz + WONK axis) or Newsreader italic display; body Source Serif 4 or Figtree
- Seeds: `#FAF7F2` paper · `#1C1A17` ink · `#C24A2C` oxide accent · `#EBE6DD` rule/surface · `#67625D` muted
- Shape: radius 0–4px, hairline borders (1px, low-contrast), shadows nearly absent
- Motion: page-like — fades and small vertical settles, 250ms
- Fits: content products, newsletters, research tools, premium calm
- Signature ideas: drop caps, numbered sections, pull-quote components

### Neo-Brutalist
Loud, honest, hand-drawn energy. Everything outlined, nothing subtle.
- Type: Space Grotesk or Archivo Black display; body Space Grotesk/Inter
- Seeds: `#FFFDF5` bg · `#000000` ink · `#FF5D5D` `#2F6BFF` `#FFD23F` unapologetic accents
- Shape: 2px solid `#000` borders on everything, radius 0–8px, **hard offset shadows** (`4px 4px 0 #000`), no blur anywhere
- Motion: snappy 120ms, translate the shadow on press (element moves into it)
- Fits: dev tools, indie products, brands that want to look hand-built
- Risk: itself now a trend — earn it with real voice in the microcopy, or skip

### Soft-Depth Dark (product dark mode done right)
Near-black blue-tinted surfaces, elevation by lightness, one electric accent.
- Type: Geist or Inter; Geist Mono/JetBrains Mono for data
- Seeds: `#0F1014` bg · `#16171D` surface · `#1D1E26` raised · `#E6E7EB` text · `#9A9CA6` muted · one accent e.g. `#7C7CF5`
- Shape: radius 8–10px, borders `rgba(255,255,255,0.08)`, shadows barely visible — depth comes from surface lightness steps
- Motion: 200–300ms ease-out, subtle accent glow on focus
- Fits: dev tools, pro/power software, dashboards
- Risk: the entire dev-tool industry looks like this — the accent hue and one signature element must do the differentiating

### Warm Humanist
Friendly without being childish; the "well-lit studio" feeling.
- Type: Fraunces or Bricolage Grotesque display; body Nunito Sans, Figtree, or Hanken Grotesk
- Seeds: `#FBF6EF` bg · `#2A2320` ink · `#C96F4A` terracotta · `#7D9B76` sage · `#E9DFD2` surface
- Shape: radius 10–16px, soft low shadows (2 layers, warm-tinted), 1px warm borders
- Motion: gentle 250ms ease-out, slight scale on cards (1.01)
- Fits: consumer wellness, education, community, food
- Risk: mushy hierarchy — keep ink truly dark and accents disciplined

### Terminal / Phosphor
Monospace everything, CRT energy, information as aesthetic.
- Type: JetBrains Mono or IBM Plex Mono everywhere (display = heavier weight, larger, tighter)
- Seeds: `#0A0E0A` bg · `#33FF66` phosphor (or `#FFB000` amber) · `#122012` surface · `#7BAF8A` muted · `#FF4D4D` alert
- Shape: radius 0, 1px borders in the phosphor at 25% alpha, no shadows; optional scanline overlay at 3% opacity
- Motion: stepped/instant, cursor blinks, text can "type on" for one signature moment
- Fits: CLIs, security, crypto-infra, anything wanting hacker credibility
- Risk: contrast math is unforgiving on saturated greens — verify every pair

### Bauhaus / Geometric
Primary colors, geometric forms, playful rigor.
- Type: Jost or Outfit (geometric sans); Archivo Black for display punch
- Seeds: `#F5F1E8` paper · `#1A1A1A` ink · `#BE1E2D` red · `#21409A` blue · `#FFDE00` yellow
- Shape: circles/quarter-circles as decorative motifs, radius either 0 or full (nothing between), 2px borders
- Motion: rotational/translational — shapes slide and rotate, 300ms ease-in-out
- Fits: creative tools, kids' education done smart, brand-forward marketing

### Luxury / Fashion
High contrast serif, letterspaced caps, extreme restraint.
- Type: Bodoni Moda (opsz) display; body Jost or Lora; labels in letterspaced small caps (+0.12em)
- Seeds: `#F6F3EE` ivory · `#0E0E0E` near-black · `#B99754` gold used almost never · `#DDD6CB` rule
- Shape: radius 0, hairlines, no shadows; huge imagery, huge whitespace
- Motion: slow (400–500ms), long-distance fades, nothing bounces — ever
- Fits: premium e-commerce, hospitality, portfolio of high-end work
- Risk: dies instantly with cramped spacing — sections need 120px+ air

### Industrial / Utilitarian
Dense, labeled, engineered. Beauty from precision, not decoration.
- Type: IBM Plex family (Sans + Mono; Serif optional) — the superfamily is the point
- Seeds: `#F4F4F2` bg · `#17191B` ink · `#FF6A00` safety orange · `#3E5C76` steel · `#D9D9D4` grid lines
- Shape: radius 0–4px, visible 1px grid/rules, tags and stamps as UI elements, tabular numerals everywhere
- Motion: functional only — 150ms, no easter eggs
- Fits: logistics, manufacturing, analytics, ops tools
- Signature ideas: small-caps section labels (`SECTION 04 / SHIPMENTS`), spec-sheet layouts

### Playful / Toy
Rounded everything, candy color, springy physics.
- Type: Bricolage Grotesque or Baloo 2 display; body Nunito or DM Sans
- Seeds: `#FFF8F0` cream · `#292F36` ink · coral `#FF6B6B` · teal `#3FBFB2` · sun `#FFCA3A` (shift hues per product — this trio is well-worn)
- Shape: radius 16–24px or full pills, chunky 2px borders in ink, "sticker" shadows (offset, same-hue)
- Motion: springs (overshoot ~1.05), staggered pops, 250–350ms
- Fits: consumer social, kids, gamified habit products
- Risk: legibility — ink must stay near-black and body type ≥16px

### Aurora / Glass
Translucent layers over gradient meshes. **Highest slop risk in this list** — this is the AI-default look. Only choose it deliberately, and subvert at least one convention.
- Type: something with character — Sora or Schibsted Grotesk (not Inter, or it's the full cliché)
- Seeds: `#0B0D12` base · mesh from `#7C3AED` `#22D3EE` `#E879F9` at low opacity · text `#EDEEF2`
- Shape: `backdrop-filter: blur(20px)`, 1px `rgba(255,255,255,0.12)` borders, radius 12–16px
- Motion: slow ambient mesh drift (20s loops), content itself moves normally
- Rule: glass for max two surface types; solid surfaces do the work

### Retro-Soft (70s warmth)
Chunky curves, sun-baked palette, optimistic.
- Type: Fraunces 900 with WONK=1 (excellent Cooper-Black energy); body Work Sans
- Seeds: `#F7EDD9` cream · `#4A3527` espresso ink · `#E07A2F` orange · `#D9A441` mustard · `#8A8F3C` avocado
- Shape: radius 12–20px, thick borders in ink, flat or paper-grain surfaces, arch/sunrise motifs
- Motion: easygoing 300ms, slight rotation wiggles on hover for one signature element
- Fits: coffee/food, music, lifestyle brands, anything anti-corporate

## 3. The signature element

Every direction must name **one** memorable thing — the element someone would describe to a friend. One, not three; a signature diluted is a signature lost. Examples of the *category*:

- A structural motif (ledger hairlines everywhere; everything in numbered sections)
- A distinctive interaction (the press that moves a card into its own shadow; type-on text)
- An ownable color behavior (the UI is monochrome until data arrives, then data is the only color)
- A typographic move (oversized wonky serif numerals; small-caps labels on every region)

The signature appears in the direction demo, survives into the system as named tokens/components, and the crit protocol checks it's still present in every screen.

## 4. Anti-slop protocol

Generated design converges on a recognizable median. Scan every direction and every screen against this list — any hit must be deliberate and defensible, or it goes:

1. Inter/Poppins + purple-to-blue gradient + glassmorphism cards — the median itself
2. Every section centered; hero → 3 feature cards → testimonials → CTA scroll template
3. Uniform border-radius and identical shadow on every element
4. Gradient text on headlines; emoji as icons
5. Purple/indigo as "default tech accent" chosen by no one
6. Fake trust signals: invented logos, "Trusted by 10,000+ teams", stock testimonials
7. Lorem ipsum, "John Doe", `user@example.com`, round numbers everywhere ($100, 50%, 1,000)
8. Identical 3-column icon-title-blurb feature grids
9. Placeholder gray boxes where imagery should be — design the image treatment instead
10. Dark mode as pure inversion (`#000` + neon) rather than a designed palette

Counter-moves: pick one signature and quiet everything else; use an accent hue nobody defaults to (oxide, phosphor, safety orange, oxblood, moss); let type do work shadows were doing; left-align more than feels comfortable; write real microcopy early — words are the cheapest distinctiveness.

## 5. Typeface pairing shortlist

Safe to load from Google Fonts, chosen for character (skip the exhausted: Playfair+Montserrat, Bebas Neue, Poppins-everything, Lobster):

| Display | Body | Data/Mono | Feeling |
|---|---|---|---|
| Fraunces (opsz, wonk) | Figtree | JetBrains Mono | warm editorial product |
| Newsreader italic | Work Sans | — | literary, calm |
| Space Grotesk | Inter | IBM Plex Mono | techy with a pulse |
| Bricolage Grotesque | Hanken Grotesk | — | contemporary, friendly |
| Instrument Serif | Instrument Sans | — | fashion-adjacent product |
| Archivo (tight, 700+) | Source Serif 4 | Spline Sans Mono | newsroom |
| IBM Plex Sans | IBM Plex Sans | IBM Plex Mono | industrial superfamily |
| Bodoni Moda | Jost | — | luxury |
| Syne (700) | DM Sans | — | art-forward |
| JetBrains Mono (700) | JetBrains Mono | itself | terminal |

Rules: max two families plus an optional mono; pair by contrast (serif+grotesk, display+humanist), never two similar grotesks; Inter is genuinely good but it's the default of defaults — if chosen, the distinctiveness budget moves entirely to color/layout/signature.

## 6. The direction demo (`02-direction.html`)

Spec for the comparison artifact:

- Three columns (CSS grid, stack under 900px), each column fully in its own direction: its Google Fonts, its seeds, its shape language — three tiny worlds on one page
- Each column = direction name + one-liner + signature callout, then a **mini render of the founder's actual key screen**: their product name, their real primary task, 2–3 real UI elements (nav fragment, primary button, one card/row with realistic data)
- Each column footer: the 5 seed swatches with hex labels + the typeface names
- No shared styling between columns beyond layout scaffolding; the page's own chrome stays neutral (system font, white) so it never competes
- Before presenting: `color.py check` on each direction's ink/bg and accent/bg pairs — print the grades into each footer (e.g. `ink on paper 14.2:1 AAA`) — accessibility shown off as craft, not compliance
