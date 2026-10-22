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
- **Verified Green** (`good`): supported.
- **Amber Note** (`warm`): misquoted, in progress, rate limited.
- **Muted Red** (`bad`, lifted to read 4.5:1 on a panel): contradicted.
- **Smoke** (`ink-muted`): not found, no citation, unavailable, needs a human.

**The Word First Rule.** A status is always its word ("contradicted"); colour never stands alone.
**The One Voice Rule.** Coral appears on at most one action per screen; red belongs to "contradicted" only.

## Typography

**Display Font:** Source Serif 4, with Georgia
**Body Font:** Inter, with system-ui
**Label/Mono Font:** JetBrains Mono for sources, line numbers and the trace

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

## Elevation & Depth

Flat. Depth comes from three tones (canvas, surface, surface-sunk) and hairlines; no drop shadows. The
trace drawer gets a soft scrim over the page behind it, like a music app's up-next shelf.

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
- **Motion:** expands from its row (height and opacity) over 420ms on `cubic-bezier(0.2, 0, 0, 1)`, like
  a music app's mini-player growing into the full player; collapses in 300ms. Mismatched words highlight after
  the panel settles, 200ms later.

### Trace drawer
- **Motion:** slides up from the bottom over 480ms ease-out with a 240ms scrim fade (a music app's up-next
  shelf).

### Buttons
- **Primary:** coral pill, black label; hover lifts brightness, focus shows a 2px coral ring.

## Do's and Don'ts

### Do:
- **Do** keep every screen dark; light only on request.
- **Do** give each moving element its own motion (rise, crossfade, expand, slide); 280-480ms; all off under reduced motion.
- **Do** pair every status colour with its word.

### Don't:
- **Don't** use springs, bounces or sub-250ms moves for structural changes (Luis: too fast).
- **Don't** reuse one fade for everything (Luis: all the same motion).
- **Don't** use coral and red together on one element.
