# Solvent — Screen Inventory

Priority order, derived from the brief's top tasks. All screens consume the `:root` token block from `03-design-system.html` verbatim. Mockup shortcuts: `g` = 8px grid overlay, `b` = squint test.

## 1. dashboard — built
Purpose: answer "how long do I have?" in under 3 seconds, without interaction.
Effortless thing: reading the runway number — it's the largest object on the page, above the fold, always current.
Layout: top nav 56 / content max 960 — runway hero + stat columns on ledger lines, recent entries below.
Density: comfortable
States in mockup: default · empty (first-run)
Microcopy: label "Months of runway" · display "14.2" · sub "Solvent until Sep 2027 — recomputed 4 minutes ago" · primary "Add transaction" · empty title "Your ledger is empty" · empty body "Add your first transaction or connect Stripe, and Solvent starts counting your months."

## 2. transactions — built
Purpose: review and trust the ledger; make anomalies obvious without alarm.
Effortless thing: scanning amounts — right-aligned tabular column, month-grouped, hairline rows.
Layout: top nav / content max 960 — toolbar (search + filters + add), month-grouped ledger table.
Density: compact (data screen earns it — rows 40px, 14px type)
States in mockup: default · row-level badges (Estimate, Failed sync) · truncation case
Microcopy: h1 "The ledger" · search placeholder "Search payees…" · count "128 entries · May – Jul 2026" · failed-sync badge "Failed sync" with row action "Retry"

## 3. assumptions — built
Purpose: change what Solvent believes (burn, income, cash) and see runway recompute instantly.
Effortless thing: the feedback loop — edit a number on the left, the runway preview updates on the right, no save-and-pray.
Layout: top nav / content max 960 — form column (max 420) + sticky preview card rail.
Density: comfortable
States in mockup: default · field error · unsaved-changes bar
Microcopy: h1 "Your assumptions" · helper "Solvent observes your ledger; override anything it got wrong." · error "That doesn't parse as an amount — try 3200 or 3,200.00" · unsaved bar "Unsaved changes — runway preview reflects them." · primary "Save assumptions" · ghost "Reset to observed"

## Deliberately not in v1 (see handoff · anti-invention)
auth/onboarding flow beyond the empty state · settings/billing · dark mode · mobile bottom-nav pattern (v1 keeps top nav at all widths)
