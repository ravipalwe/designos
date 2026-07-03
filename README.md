# DesignOS

**A complete design operating system for AI agents.** Takes a product from raw idea to dev-ready design through five gated phases — with senior-level craft encoded, contrast mathematically verified, and a self-critique protocol that runs before you ever see the output.

Built for designers and founders who want designed products, not template output.

## Install

```bash
npx skills add ravipalwe/designos
```

On the marketplace: [skills.sh/ravipalwe/designos](https://skills.sh/ravipalwe/designos)

Works with any agent that reads `SKILL.md` — Claude Code, Cursor, Windsurf, Amp, Devin, and friends. Then just say:

> run DesignOS on my app idea

## What it does

```
Brief → Direction → Design System → Screens → Handoff
```

| Phase | You get | Gate |
|---|---|---|
| **1 · Brief** | Taste profile (5 axes), users, top tasks, constraints | quick confirm |
| **2 · Direction** | 3 genuinely distinct directions rendered **on your own product** in one HTML file — pick one, mint 3 design principles + a signature element | hard gate, never skipped |
| **3 · Design System** | Full token spec (OKLCH-built color ramps, type matrix, spacing, motion) as YAML + a live HTML style guide, every contrast pair verified | review & refine |
| **4 · Screens** | One self-contained HTML mockup per screen — real content, real states, wired focus/hover, built only from system tokens | per screen |
| **5 · Handoff** | Token export (CSS `light-dark()` / Tailwind `@theme` / DTCG JSON), dependency-ordered build checklist, acceptance criteria, design-QA loop | done |

Everything lands in a `design/` directory. `design/STATE.md` tracks every decision, so you can stop mid-process and resume days later — in a fresh session — with zero re-explaining.

## Why it's different

**Verified, not asserted.** Ships with `scripts/color.py` (zero dependencies): WCAG 2.1 + APCA contrast checking with auto-fix suggestions, perceptually-even OKLCH ramp generation, hex→OKLCH inspection. The skill is forbidden from claiming contrast it hasn't computed.

```
$ python3 scripts/color.py check "8A8580 FAF7F2 muted"
label  fg       bg       WCAG    grade  need     APCA Lc  need    apca  verdict  suggestion
muted  #8A8580  #FAF7F2  3.42:1  AA-lg  4.5 req  +59.5    75 req  low   FAIL     try fg #67625D
```

(That failing pair was in this skill's own first draft — the script caught it before shipping. That's the loop working.)

**Anti-generic by design.** A taste-calibration step, 12 named style worlds with real recipes, an anti-slop scan targeting the recognizable AI-median look (Inter + purple gradient + glass cards), and a "one signature element" discipline so every product has the thing you describe to a friend afterward.

**Crit before present.** A 10-pass critique protocol — squint test, alignment walk, rhythm check, state completeness, slop scan, a11y pass — runs on the agent's own output *before* the human sees it.

**Craft encoded, loaded just-in-time.** Six reference files carry the knowledge (OKLCH hue-drift ramps, concentric radii, two-layer tinted shadows, type-scale matrices, motion choreography, content-first screen design) and are read only at the phase that needs them — the skill stays lean in context.

**Mockups you can interrogate.** Every screen ships with a dev overlay: press `g` for an 8px grid, `b` for a live squint test. Self-contained HTML — opens straight from disk, no build step.

## Package

```
skills/designos/
  SKILL.md                  the conductor — phases, gates, modes, state
  references/
    direction.md            taste axes · 12 style worlds · anti-slop protocol
    foundations.md          color/OKLCH · typography · spacing · depth
    motion.md               duration & easing tokens · choreography
    screens.md              content-first method · real-data rules · craft bar
    critique.md             the 10-pass crit protocol
    handoff.md              token exports · build order · design-QA loop
  scripts/
    color.py                WCAG 2.1 + APCA + OKLCH — stdlib only, no deps
```

Modes: fresh start · resume · revision (names downstream cost first) · redesign of an existing product · brand intake (builds around your existing brand) · fast mode ("just run it").

## Example

[`examples/solvent/`](examples/solvent/) — DesignOS run on a demo product (Solvent, a runway tracker for bootstrapped founders). Open [`design/02-direction.html`](examples/solvent/design/02-direction.html) to see the direction gate: three worlds rendered on the product's own dashboard, contrast grades printed in each footer.

## Requirements

- File-system access (writes the `design/` directory)
- `python3` for the color script (no packages needed)
- Optional: Figma MCP for reading Figma references; browser tooling for visual self-verification

## Security

- `scripts/color.py` is pure stdlib — no network calls, no file writes, no dependencies to audit.
- Like every agent skill, DesignOS runs with your agent's permissions. It's all readable markdown — read it before you run it.

## License

MIT © Ravi Palwe
