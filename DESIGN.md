---
version: alpha
name: "Receipts"
description: "Dark-first fact-check reading room: an editorial serif and warm coral on a near-black stage."
colors:
  canvas: "#030303"
  surface: "#1f1f1f"
  surface-sunk: "#0e0e11"
  line: "#303030"
  ink: "#ffffff"
  ink-muted: "#aaaaaa"
  accent: "#cc785c"
  good: "#5db872"
  warm: "#d4a017"
  bad: "#d16868"
  highlight: "rgba(212,160,23,0.18)"
  chip-border-alpha: "0.4"
typography:
  display:
    fontFamily: "Source Serif 4, Georgia, serif"
    fontSize: 44px
    fontWeight: 400
    lineHeight: 1.1
    letterSpacing: -0.02em
  title:
    fontFamily: "Source Serif 4, Georgia, serif"
    fontSize: 26px
    fontWeight: 400
    lineHeight: 1.25
    letterSpacing: -0.01em
  body:
    fontFamily: "Inter, system-ui, sans-serif"
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.5
  label:
    fontFamily: "Inter, system-ui, sans-serif"
    fontSize: 13px
    fontWeight: 600
    lineHeight: 1.25
  mono:
    fontFamily: "JetBrains Mono, ui-monospace, monospace"
    fontSize: 13px
    fontWeight: 400
    lineHeight: 1.5
motion:
  ease-rise: "cubic-bezier(0.22, 1, 0.36, 1)"
  ease-panel: "cubic-bezier(0.2, 0, 0, 1)"
  row-enter: 360ms
  row-stagger: 60ms
  chip-change: 280ms
  panel-open: 420ms
  panel-close: 300ms
  highlight: 320ms
  drawer: 480ms
  scrim: 240ms
  shimmer-cycle: 1.6s
rounded:
  sm: 4px
  md: 8px
  lg: 14px
  pill: 9999px
spacing:
  xs: 8px
  sm: 16px
  md: 24px
  lg: 32px
components:
  claim-row:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink}"
    typography: "{typography.body}"
    rounded: "{rounded.md}"
    padding: 12px 16px
  status-chip-supported:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.good}"
    typography: "{typography.label}"
    rounded: "{rounded.pill}"
    padding: 6px 10px
  status-chip-contradicted:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.bad}"
    typography: "{typography.label}"
    rounded: "{rounded.pill}"
    padding: 6px 10px
  status-chip-misquoted:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.warm}"
    typography: "{typography.label}"
    rounded: "{rounded.pill}"
    padding: 6px 10px
  status-chip-neutral:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink-muted}"
    typography: "{typography.label}"
    rounded: "{rounded.pill}"
    padding: 6px 10px
  status-chip-needs-human:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink}"
    borderStyle: dashed
    typography: "{typography.label}"
    rounded: "{rounded.pill}"
    padding: 6px 10px
  status-chip-in-progress:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink-muted}"
    typography: "{typography.label}"
    rounded: "{rounded.pill}"
    padding: 6px 10px
  receipt-panel:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink}"
    typography: "{typography.body}"
    rounded: "{rounded.lg}"
    padding: 24px
  button-primary:
    backgroundColor: "{colors.accent}"
    textColor: "{colors.canvas}"
    typography: "{typography.label}"
    rounded: "{rounded.pill}"
    padding: 10px 18px
---

# Design System: Receipts

<!-- Source: Luis's taste-picker rounds 1-3 (2026-10-22): two picked references, an editorial AI assistant
and a music-streaming app, on the Luis Dark base. Brand names and brand fonts are left out of this public file. -->

## Overview

**Creative North Star: "The Night Reading Room"**

A report's claims laid out like liner notes on a black stage: a literary serif and warm coral
give the words weight, a near-black canvas and soft charcoal panels keep everything else
quiet. Dense enough to scan a whole report at a glance, calm enough to read a receipt line by line.
Dark is the only theme unless Luis asks for light.

**Key Characteristics:**
- Near-black stage (#030303) with charcoal panels; depth from tone, not shadow.
- One warm accent, coral (#cc785c), for the single primary action and focus.
- Serif for what a person reads as a statement (headings, the claim in a receipt); sans for the interface.
- Every status is a word in a pill; colour only reinforces it.
- Motion is unhurried and specific to each element (Luis, round 3: the samples were "too fast" and "all the same").

## Colors

A black stage, charcoal surfaces, one coral voice, and four state colours that always travel with a word.

### Primary
- **Warm Coral** (#cc785c): the one primary action per screen, focus rings, the active row's edge. 6.3:1 on the canvas.

### Neutral
- **Stage Black** (`canvas`): the page. Near-black, deeper than Luis Dark's ground.
- **Charcoal Panel** (`surface`): claim rows, the receipt panel, chips' fill.
- **Sunk Well** (`surface-sunk`): the source-line well inside a receipt, the trace drawer.
- **Hairline** (`line`): row dividers and panel borders, 1px.
- **Paper White** (`ink`): primary text.
- **Smoke** (`ink-muted`): sources, timestamps, metadata; 7.1:1 on a panel.

### States
Labels (verdicts) get a state colour; statuses (no verdict) stay neutral, so a colour always means a verdict.
- **Verified Green** (`good`): supported, and the "verified in source" mark.
- **Amber Note** (`warm`): misquoted, and the mismatch highlight (`highlight`).
- **Muted Red** (`bad`, lifted to read 4.5:1 on a panel): contradicted.
- **Smoke** (`ink-muted`): not found, plus the statuses no citation, unavailable and rate limited.
- **Needs a human**: paper-white text in a dashed pill, so the default "needs review" view can tell it from "not found".
- **In progress** (waiting, fetching, finding the passage, checking the quote): a smoke pill with the step's word; the row's shimmer carries the "live" feeling.

Every chip has a 1px border in its text colour at 40% (`chip-border-alpha`).

**The Word First Rule.** A status is always its word ("contradicted"); colour never stands alone.
**The One Voice Rule.** Coral fills at most one action per screen; focus rings and the open row's edge are coral outlines, never fills. Red belongs to "contradicted" and the injection note only.

## Typography

**Display Font:** Source Serif 4, with Georgia
**Body Font:** Inter, with system-ui
**Mono Font:** JetBrains Mono for sources, line numbers and the trace

**Character:** an editor's serif for statements over a plain humanist sans for the tool around them.

### Hierarchy
- **Display** (400, 44px, 1.1, -0.02em): the report title, once per screen.
- **Title** (400, 26px, 1.25): a receipt's claim, quoted.
- **Body** (400, 16px, 1.5): row text and receipt prose, 65-75ch max.
- **Label** (600, 13px): chips, buttons, column heads.
- **Mono** (400, 13px): source lines, links, trace steps.

**The Serif Speaks Rule.** Serif only for words someone said or wrote; the interface stays sans.

## Layout

Single column of claim rows, 8px rhythm (`xs` to `lg`), 16px side gutter on phones. A receipt opens in
place under its row on phones and as a side panel at desktop width; the full trace is a bottom drawer.

**Picked layout (Luis, 2026-10-22): the side panel.** Of four report-view variations (inline, side panel,
bottom sheet, pulled quote), Luis chose the side panel: claim rows on the left, the open receipt in a
420-480px panel on the right that slides in from the right (420ms, `cubic-bezier(0.2, 0, 0, 1)`). Every
screen uses it at 1024px and wider; below that the receipt opens under its row.

## Elevation & Depth

Flat. Depth comes from three tones (canvas, surface, surface-sunk) and hairlines; no drop shadows. The
trace drawer gets a soft scrim over the page behind it, like a music app's up-next shelf.

## Motion catalogue

Luis approved this set on 2026-10-22 ("The motion feels right"). Each element has its own motion.
Structural moves (rows, chips, panels, drawers) stay within 280-480ms; fills, sweeps and cycles run
slower because they show progress, not structure.

| Element | Motion | Timing |
| --- | --- | --- |
| Headline | Each line wipes up from a clip, 120ms apart | 480ms, `ease-rise` |
| Claim rows | Rise 12px and fade, 60ms apart | 360ms, `ease-rise` |
| Row being checked | A faint coral reading band moves across the claim text, plus a shimmer on the bottom hairline | 2.4s and 1.6s loops, linear |
| Status chip | Old word slides up and out, new word slides up and in | 280ms, ease-out |
| Landing demo chip | Waiting → Fetching the source → Checking the quote → Supported | one step every 1.2s |
| Progress bar | Fills in steps, one per claim | stepped |
| Stat values | Tick up from below a mask, 80-90ms apart | 420ms |
| Receipt panel | Slides in from the right | 420ms, `ease-panel` |
| Agent steps | Appear one by one from the left, 160ms apart | 300ms each |
| Verified mark | Its tick draws itself | 360ms |
| Source line | A coral frame wipes closed around the matched line after verification | 420ms |
| Mismatch highlight | Sweeps across the differing words after the panel settles | 320ms |
| Trace bars | Waterfall: each bar starts where the last ended; the step name brightens when its bar finishes | 900ms each |
| Worst-mistake number | Flips down into place | 420ms |
| Recommended chip | One light sweep | 700ms |
| Hover | Coral hairline on rows, brighter buttons, link arrows nudge 3px | 200ms, ease |

Design mock-ups on the canvas loop on a 6-second cycle (play, hold about 4s, reset) so the motion can be
judged without reloading. In the product, entrances play once, and the live indicators (reading band,
shimmer, demo chip) run only while a claim is being checked. Under reduced motion every row above falls
back to its end state, as described under Accessibility.

## Shapes

Gently curved panels (8px rows, 14px receipt panel), fully round pills for chips and buttons, square 4px corners only on inline code.

## Components

### Claim row
- **Shape:** 8px corners, charcoal panel, hairline divider.
- **Content:** the claim (body), source in mono smoke, status chip on the right.
- **Motion:** enters with a 360ms rise (12px) and fade on `cubic-bezier(0.22, 1, 0.36, 1)`, staggered
  60ms per row; while checking, a slow 1.6s shimmer runs along its bottom hairline.

### Status chip
- **Style:** pill, charcoal fill, the state colour as text and a 40% border.
- **Motion:** a state change crossfades the colour over 280ms and the word slides up 6px; it never bounces.

### Receipt panel
- **Shape:** 14px corners, 24px padding; the source line sits in a sunk well.
- **Motion:** at 1024px and wider it slides in from the right over 420ms on `cubic-bezier(0.2, 0, 0, 1)`;
  below that it expands from its row (height and opacity) over the same 420ms, like a music app's
  mini-player growing into the full player. Either way it closes in 300ms. Mismatched words highlight after
  the panel settles, 200ms later.

### Receipt marks (PRD FR2a-FR2d)
- **Mismatch highlight:** differing words get `highlight` behind amber text plus a 2px underline, so it reads without colour.
- **Verified in source:** a small `good` pill in the source well, with the word.
- **Evidence strength:** "evidence: strong" or "evidence: partial" in mono smoke beside the label.
- **Injection note:** a dashed `bad`-bordered note inside the receipt reading "this source tried to instruct the checker"; the claim's chip is "needs a human".

### Trace drawer
- **Motion:** slides up from the bottom over 480ms ease-out with a 240ms scrim fade (a music app's up-next
  shelf).

### Buttons
- **Primary:** coral pill, black label; hover lifts brightness, focus shows a 2px coral ring.

## Accessibility

Text contrast on the dark tones (WCAG 2.2 AA asks 4.5:1 for text):

| Text | On | Ratio |
| --- | --- | --- |
| ink-muted #aaaaaa | surface #1f1f1f | 7.1:1 |
| warm #d4a017 | surface | 6.9:1 |
| good #5db872 | surface | 6.7:1 |
| bad #d16868 | surface | 4.6:1 (no room to darken the surface) |
| coral #cc785c | canvas #030303 | 6.3:1 |
| coral | surface | 5.0:1 |
| canvas #030303 on a coral button | | 6.3:1 |

Focus: a 2px coral ring with a 2px offset on every focusable thing, rows and chips included (PRD FR5).

**Reduced motion.** Each motion has a still fallback: rows appear in place; chips swap words instantly;
the checking row shows its step word ("checking the quote") with no shimmer; the receipt panel and
drawer appear without sliding and the scrim shows at once; highlights are present from the start; the
headline, stat values, verified mark, source frame, trace bars and recommended chip show their end state;
the progress bar and demo chip change without transitions.

## Do's and Don'ts

### Do:
- **Do** keep every screen dark; light only on request.
- **Do** give each moving element its own motion (rise, crossfade, expand, slide); 280-480ms; all off under reduced motion.
- **Do** loop motion in design mock-ups (play, hold, replay) so it can be judged without reloading.
- **Do** pair every status colour with its word.

### Don't:
- **Don't** use springs, bounces or sub-250ms moves for structural changes, meaning rows, chips, panels and drawers (Luis: too fast). Stagger offsets, delays, the scrim fade and the looping shimmer are not structural moves.
- **Don't** reuse one fade for everything (Luis: all the same motion).
- **Don't** use coral and red together on one element.
