# Handoff: PM Homework Presentation (Playbook + Applied Case)

## Overview
A single scrolling landing page presenting a product-decision method ("the Playbook": 8 gated stages) and a real applied case study (Enefit, a Baltic energy retailer, choosing its next B2C package). Built for a PM job-application take-home, meant to be self-explanatory in plain language, click-through, with voiceover-friendly pacing.

## About the Design Files
The bundled file (`index.html`) is a **design reference** — a working React/JSX prototype (single HTML file, in-browser Babel) showing the intended look, content, and behavior. It is not meant to be shipped as-is into a production codebase. If recreating this in a target app, rebuild the structure and interactions using that app's existing framework and design system (React, Vue, etc.), or pick the most suitable framework if none exists yet.

## Fidelity
**High-fidelity.** Colors, typography, spacing, copy, and interaction behavior are final as designed. Recreate pixel-close using the target codebase's component/styling conventions.

## Screens / Views
This is one continuous page with four sections, navigated via a sticky top nav with anchor links (`#playbook`, `#exercise`, `#applied`). Stage 2 (`#stage2`), Stage 3 (`#stage3`), Cheap Tests / Stage 4 (`#cheap-tests`) and Stages 5-8 (`#stages-5-8`) are not separate primary-nav items — they're all a continuation of the Applied section (Enefit's live run, Stages 2 through 8), sitting directly below it with no visual break. A secondary, in-page "jump to" sub-nav (five pill links: Stage 1 · Opportunity / Stage 2 · Discovery / Stage 3 · Hypotheses / Stage 4 · Cheap tests / Stages 5–8) sits at the top of the Applied section itself, giving a reviewer a way to skip directly to any of these sub-sections without scrolling past the whole run.

### 1. Hero
- **Purpose**: Opening framing statement.
- **Layout**: Full-width dark section, radial gradient blobs + dot-grid texture background, centered content column max-width 820px, generous top/bottom padding (~110px/96px).
- **Components**:
  - H1, 48px, Space Grotesk 700, line-height 1.15, white, max-width 640px.
  - Subhead paragraph, 19px, IBM Plex Sans, color `oklch(80% 0.01 260)`.
  - Two pill CTAs ("See how it works" / "Jump to the real case") — filled teal accent and outlined dark variants, 100px border-radius, hover lifts with shadow.
  - Fades/slides in on mount (translateY 16px → 0, opacity 0→1, 0.8s cubic-bezier(.16,1,.3,1)).

### 2. The Playbook (`#playbook`)
- **Purpose**: Explain the general 8-stage decision framework.
- **Layout**: Light background (`oklch(97.5% 0.006 255)`), max-width 1080px centered column.
- **Components**:
  - Section intro: centered heading + subhead, max-width 680px.
  - **Stage list** (8 items), each a horizontal row: left column is a circular numbered badge (52px, gradient teal fill, drop shadow, scale-only hover) connected by a vertical gradient line to the next stage; right column is a white card (16px radius, subtle shadow) containing:
    - Stage title (17px, Space Grotesk 600) + italic question line (14px).
    - "Produces:" and "Gate:" lines, plain text.
    - "View delivery template →" outlined pill button — opens a modal (see Interactions).
    - Always-visible "What the agent does" steps list, bulleted.
  - Each stage card and the rule/role cards scroll-reveal (IntersectionObserver-driven fade+slide-up, translateY 24px→0).
  - **Gate mechanism diagram**: white rounded panel, 3-step horizontal flow (Evidence in → Checked against a bar → GO/HOLD/STOP colored tags) with arrow glyphs between. GO and STOP render as light-tint background / dark-ink text (matching how HOLD already did it) rather than white-on-saturated, to clear WCAG AA contrast.
  - **Four rules grid**: 2×2 (responsive auto-fit) card grid, each with bold title + description.
  - **Who does what** panel: 2-column split — "An agent can do alone" (green-tinted) vs "Always needs a person" (red-tinted).

### 3. This Exercise (`#exercise`)
- **Purpose**: Explain how the take-home was actually run, and its limitations.
- **Layout**: Full-width dark section (same gradient as hero), centered column max-width 820px.
- **Components**:
  - Heading: "I didn't just describe the Playbook — I ran it."
  - 3-card row: approach bullets (picked a live case / public data only / sized two candidates).
  - "Where this exercise stops short" — 4 limitation rows (dot marker + bold title + description), dark cards.

### 4. Applied to a Real Case (`#applied`)
- **Purpose**: Show Stage 1 of the Playbook run for real on Enefit.
- **Layout**: Light background, max-width 1080px.
- **Components**:
  - Scope cards row: Who / Budget (€50,000) / Bar to clear (€500,000/yr).
  - **Opportunity scoring**: 3 horizontal progress bars (Candidate A/B/C), animated width fill on reveal, teal for sized candidates, gray for the parked one, plus an info callout below.
  - **Candidate sizing card**: toggle pill-tabs to switch between Candidate A and B; card shows:
    - Name + one-line summary.
    - Three-up comparative stat row: Worst case (19px) / Realistic yearly payoff (26px, teal, the visual emphasis) / Best case (19px) — all Space Grotesk, replacing what was previously an isolated 52px hero number with a small "worst case X · best case Y" caption underneath.
    - Animated horizontal gauge bar with a fixed "target" tick line at 50% (representing the €500k bar) and % label.
    - 3-column grid: How hard to build / Biggest open question / Legal risk.
  - **The call**: 3 recommendation cards (tag pill + title + body) — "Move forward" (A), "Hold, narrowly" (B), "Not sized" (C). This is the section's actual conclusion; a separate "Where the discovery budget should go" panel (dark gradient box, originally an animated 80/20 split bar) was removed — it only restated what the recommendation cards already said, and once a single candidate is funded a 100%-filled split bar has nothing left to compare.

### 4a. Stage 2 & Stage 3 placeholders (`#stage2`, `#stage3`) — continuation of Applied to a Real Case
- **Purpose**: Hold the visual and structural place for Stages 2 (problem discovery) and 3 (hypothesis map) of the real Enefit run, until real run data is ready to drop in. Generic, not candidate-specific — deliberately not filled with the run's actual (partial, in-progress) findings yet.
- **Layout**: Light background, max-width 1080px, same white-card treatment as the rest of Applied (14px radius, 1px border, subtle shadow) — full visual weight, matching Stage 1 and Stage 4.
- **Components**: each is a single white card — title + one-line question (Space Grotesk 20px), a status pill top-right ("NOT YET SYNCED" for Stage 2, "NOT STARTED" for Stage 3), a description paragraph, and a gate-condition line. No candidate tabs, no data tables — those get built out when real content lands.
- **Data model**: static copy only; no state. Swapping in real content later means replacing the paragraph/gate text with what's in the run's `stage2-problem-discovery.md` / `stage3-*.md`, not restructuring the section.

### 4b. Cheap Tests (`#cheap-tests`) — continuation of Applied to a Real Case
- **Purpose**: Scaffold for Stage 4 of the Playbook, run for real on Enefit — behavioral test results per candidate, filled in live as they land (not illustrative like the modal's Stages 2-8 examples).
- **Layout**: Light background, max-width 1080px, sits directly below the `#applied` section's budget-allocation box.
- **Components**:
  - Section intro: heading + subhead stating the Stage 4 budget ceiling (€500-1,500/test, €2,000-6,000 total, approved 2026-09-21) and that the section fills in live.
  - **Candidate tabs**: the same pill-tab control and `candidate` state as the Applied section's sizing card — switching candidates there also switches the test queue shown here.
  - **Test card grid** (3 per candidate currently, auto-fit columns): each card is one queued cheap test —
    - Method name (title) + hypothesis ID/type tag (top-right).
    - Hypothesis statement.
    - Key/value rows: audience/sample, primary metric, pass threshold, kill threshold, cost.
    - Footer row: result text (placeholder: "Not yet run") + a color-coded status pill (PENDING/SUPPORTED/REFUTED/INCONCLUSIVE — gray/green/red/amber, same palette as the Playbook's GO/PIVOT/KILL badges).
  - **Gate readout**: a single info bar restating the Stage 4 gate rule (go to pilot / pivot / kill) and a derived one-line verdict for the active candidate, computed from its tests' statuses — "Pending" while every test is still `pending`, flips automatically once statuses are updated.
- **Data model**: `cheapTests` (keyed `A`/`B`, mirrors `candidates`), each test object carrying `status: 'pending'|'supported'|'refuted'|'inconclusive'`. Swapping a test's `status` and `result` to real values is the only edit needed once a test actually runs — the status pill and the candidate's gate verdict recompute automatically.

### 4c. Stages 5-8 (`#stages-5-8`) — continuation of Applied to a Real Case
- **Purpose**: Placeholder for Stages 5 (Pilot) through 8 (Scale, review, sunset) of the real Enefit run — none of these have started. Deliberately lighter-weight than Stages 1-4: this run hasn't reached them yet, so there's nothing candidate-specific to show.
- **Layout**: Light background, max-width 1080px, sits directly below Cheap Tests with no visual break — a compact vertical list, not white cards.
- **Components**: one row per stage — light-gray pill-background row (`oklch(96% 0.006 255)`, 10px radius) with the stage title (Space Grotesk 600) + its one-line question inline, and a "NOT STARTED" status pill right-aligned. Below the row list, a closing "What happens next" note (heading + forward-looking paragraph on what Candidate 1/3 do next + a "↑ Back to how the Playbook works" link to `#playbook`) replaces the flat pill rows as the page's actual ending, so the last thing a reviewer reads is forward-looking rather than a set of inert "NOT STARTED" placeholders.
- **Data model**: `LATER_STAGES`/`laterStages` — a static array of `{ title, question }` for Stage 5-8, taken verbatim from the playbook's stage-map table. No per-candidate state; becomes obsolete once the run actually reaches Stage 5 and gets its own full-weight section like Stages 1-4.

### Delivery Template Modal
- **Purpose**: Show what a stage's actual output document looks like, filled with real (Stage 1) or illustrative (Stages 2-8) example data.
- **Trigger**: Click a stage's numbered circle badge, or its "View delivery template →" button.
- **Layout**: Fixed full-screen overlay, `rgba(16,20,28,0.55)` backdrop with blur, centered white modal card (max-width 520px, max-height 85vh, scrollable), rounded 18px, shadow `0 24px 60px rgba(0,0,0,0.35)`.
- **Header**: small uppercase "Stage N · Title" label + template name, close (✕) button top-right.
- **Body**: template-tag pill (e.g. "from the Enefit case — Candidate A" or "illustrative example"), then a vertical list of key/value fields; fields can render as plain text or as a colored confidence badge (dot + bold pill) when flagged.
- **Animation**: backdrop fades in, card scales from 0.96→1 (0.25s cubic-bezier(.16,1,.3,1)).
- **Close**: click backdrop, click ✕, or press Escape.
- **Accessibility**: card carries `role="dialog"`, `aria-modal="true"`, and `aria-labelledby` pointing at the title; focus moves into the card on open and is trapped there via Tab-key interception (Shift+Tab from the first focusable element wraps to the last, and vice versa), and returns to whatever triggered the modal on close; the close button has `aria-label="Close"`; each stage's badge-circle trigger button carries a descriptive `aria-label` (e.g. "View delivery template for Stage 3: Hypothesis mapping") rather than exposing only its bare number. The doc modal (case files, evidence log, playbook) follows the same pattern.

## Interactions & Behavior
- **Sticky nav**: `position: sticky; top: 0`, blurred translucent background, anchor links scroll to sections.
- **Scroll progress bar**: 2px fixed top bar, width tracks `scrollY / (scrollHeight - innerHeight) * 100`, gradient teal→amber fill, updated on scroll (passive listener).
- **Scroll-reveal**: every major block has `data-reveal-id`; an `IntersectionObserver` (threshold 0.1, rootMargin `-40px` bottom) flips a `revealed[id]` state flag once per element, which drives opacity 0→1 / translateY 24px→0 over `0.7s cubic-bezier(.16,1,.3,1)`. A periodic re-scan (400ms) picks up newly mounted elements; a fallback timer force-reveals anything still hidden 3s after entering the viewport (defensive, prevents stuck-invisible content).
- **Candidate tabs**: click switches `candidate` state (A/B), swaps all card content, re-triggers the gauge-bar width animation.
- **Bar/gauge animations**: bars start at width 0% and animate to their target % only once their container's `data-reveal-id` has been revealed — not on load — so they animate as the user scrolls to them.
- **Modal**: `openModal(n)` sets `modalStage` then a 20ms-delayed `modalVisible: true` to trigger the CSS transition in; `closeModal()` reverses it and clears `modalStage` after 200ms so the exit transition completes before unmount.

## State Management
Component-level state (single component, no external store):
- `candidate: 'A'|'B'` — active candidate tab (prop-configurable default).
- `revealed: {[id]: boolean}` — scroll-reveal flags per `data-reveal-id`.
- `scrollPct: number` — top progress bar fill.
- `heroIn: boolean` — hero entrance animation trigger (set true ~100ms after mount).
- `modalStage: number|null` — which stage's template modal is open (null = closed).
- `modalVisible: boolean` — controls the modal's enter/exit transition independent of mount/unmount timing.

No data fetching — all content (stages, rules, approach, limitations, opportunities, candidates, recommendations, cheap-test queue) is static data defined in the component.

## Design Tokens

### Colors (OKLCH)
- Dark background: `oklch(16-19% 0.02 260)` (gradient)
- Light background: `oklch(97.5% 0.006 255)`
- Ink (body text): `oklch(18-20% 0.02 260)`
- Muted text: `oklch(42-48% 0.02 260)`
- Primary accent (teal, text/border on light bg): `oklch(45% 0.13 195)` — darkened from an earlier `52% 0.12 195` to clear WCAG AA's 4.5:1 text-contrast minimum, matching `.md-body a`'s link color. `oklch(70-72% 0.12 195)` remains for large decorative fills on dark bg, where contrast isn't the constraint.
- Success/GO: `oklch(56% 0.13 150)`
- Warning/PIVOT/HOLD: `oklch(70% 0.14 70)`
- Danger/KILL: `oklch(58% 0.17 25)`
- Card borders: `oklch(89-90% 0.006 255)`
- Card backgrounds: `#fff` (light sections), `oklch(24% 0.02 260)` (dark sections)

### Typography
- Display/headings: **Space Grotesk**, weights 500/600/700
- Body: **IBM Plex Sans**, weights 400/500/600
- Scale: H1 48px, H2 34-36px, H3 27px, card titles 15-19px, body 13-19px, micro-labels 10.5-12px uppercase

### Spacing / Radius
- Section padding: ~90-110px vertical, 24px horizontal, max-width 820-1080px content columns
- Card radius: 12-18px; pills: 100px (fully rounded)
- Grid gaps: 14-24px

### Responsive
A `max-width: 600px` breakpoint reduces section vertical padding (e.g. hero 110/96px → 64/56px) and the two large type scales (H1 48px → 32px, section H2 36/32px → 26/24px) via CSS custom properties (`--hero-pad`, `--section-pad`, `--section-pad-b`, `--exercise-pad`, `--h1-size`, `--h2-size`, `--h2-size-sm`) set on `:root` and overridden inside the media query — the inline styles reference them via `var(...)` rather than hardcoding two sets of values. Card grids already use `repeat(auto-fit,minmax(...))`, so they reflow without extra breakpoints; wide hypothesis-register tables inside modals fall back to `.md-body table { display:block; overflow-x:auto }`.

### Shadows
- Resting card: `0 1px 2px rgba(16,24,40,0.04)`
- Hover card: `0 12-16px 28-36px rgba(16,24,40,0.09-0.1)`
- Modal: `0 24px 60px rgba(0,0,0,0.35)`

## Assets
No images/icons — Google Fonts only (Space Grotesk, IBM Plex Sans via `fonts.googleapis.com`). All visual elements (gauges, badges, pills) are CSS/DOM, no SVG or raster assets.

## Files
- `index.html` — the complete design (template + logic), single file, self-contained aside from the Google Fonts link and CDN-loaded React/Babel/marked/mermaid.
