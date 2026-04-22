# DESIGN.md — Karl Qu personal site

The system that already exists in the CSS, written down so future edits stay on-brand.
If you ever disagree with something here, change the code AND update this file together.

## Voice

Editorial. Confident. No SaaS hedging. Specific nouns beat abstract verbs.
"Atoms, but with venture returns." > "Innovative investments in deep tech."
If you wrote a sentence that could appear on any other VC site, delete it.

## Color

Dark-only. There is no light theme.

| Token | Value | Use |
|---|---|---|
| `--bg` | `#0a0a0a` | Page background, everywhere |
| `--bg-elev` | `#111111` | Elevated surfaces (partners card, form labels bg) |
| `--fg` | `#f5f5f3` | Primary text, icons |
| `--fg-dim` | `#a3a3a0` | Secondary text, body prose |
| `--fg-muted` | `#6b6b68` | Tertiary text, meta, labels |
| `--line` | `#1f1f1f` | Default 1px dividers |
| `--line-strong` | `#2a2a2a` | Buttons, inputs, tag borders |
| `--accent` | `var(--fg)` | CTAs, focus rings, hover underlines |
| `--accent-ink` | `var(--bg)` | Text on accent-colored surfaces |

**Functional colors** (inline `oklch()`, not tokenized because they only appear once or twice each):
- Status / success / "do" marks — `oklch(0.75 0.15 145)` (calm green)
- Error / "don't" marks — `oklch(0.7 0.18 25)` (muted red)
- Draft indicators — `oklch(0.7 0.14 75)` (muted amber)

Rationale: palette is intentionally narrow. Adding a new color is a significant design decision — check if an existing token works first.

## Typography

Two families only:

- **Inter Tight** — all prose and display type. Weights: 300, 400, 500, 600, 700.
- **JetBrains Mono** — all structural labels, captions, metadata, nav, stats, section numbers. Weights: 400, 500.

Mono is for **structure**. Prose is for **meaning**. Don't use mono for prose or prose for labels.

### Scale

| Size | Family | Use |
|---|---|---|
| 10.5px mono | Mono 500 | Tags, role/sector chips |
| 11–12px mono | Mono 400/500 | Nav, meta bar, stat labels, captions |
| 13px mono | Mono 500 | Section title labels |
| 14–15px sans | Inter 400 | Body prose |
| 17–22px sans | Inter 500 | Sub-section headings (pitch-step h4, thesis h3) |
| 26–38px sans | Inter 500 | Section ledes, contact heading |
| 44–88px sans (clamp) | Inter 500 | Hero h1 |
| 48–140px sans (clamp) | Inter 500 | Footer big statement |

Tracking:
- Display type: `-0.025em` to `-0.035em`
- Body: `-0.005em`
- Mono labels: `0.04em` to `0.08em` (wider)

Italic is used for **accent words inside headlines only** (see "Italic accent" below).

### Italic accent

Signature move: one word per headline set in italic to act as a typographic highlight.
Examples: "I find *pre-seed* companies...", "Building something *obviously hard*?", "A 5-minute email *beats* a 45-minute deck."

Rules:
- Used only in Inter Tight, never in mono.
- `font-style: italic; font-weight: 400;` (the surrounding text is 500)
- The italicized word carries color `var(--fg)` when the surrounding text is dim, or `var(--fg-muted)` when the surrounding text is solid — inverse of its container for gentle contrast.

## Spacing

There's a scale. Use it for structural rhythm. Component-internal padding (button heights, form field padding, etc.) is tuned to match specific line-heights and may not land on a token — that's intentional.

| Token | Value | Where |
|---|---|---|
| `--space-1` | 4px | micro gaps, 1-char offsets |
| `--space-2` | 8px | tight label→value gaps |
| `--space-3` | 12px | nav gaps, cta-row gap |
| `--space-4` | 16px | standard body paragraph rhythm |
| `--space-5` | 24px | section-head → body gap |
| `--space-6` | 32px | within-section rhythm, list-row padding |
| `--space-7` | 48px | end-of-subsection breathing |
| `--space-8` | 64px | between major blocks in a section |
| `--space-9` | 96px | `--row-pad` base; section top/bottom |

Additional layout constants (pre-existing):
- `--gutter: 32px` — horizontal container padding
- `--maxw: 1100px` — container max-width
- `--row-pad: 96px` — section vertical padding on desktop (64px on mobile)
- `--radius: 2px` — the only corner radius. Do not introduce others.

**Migration policy:** prefer `var(--space-*)` for new structural spacing. Existing values like `56px`, `72px`, `40px` are kept where they're tuned to specific type rhythms. If a new requirement forces a rhythm change, update the value *and* the relevant DESIGN.md note.

## Shape & decoration

- **Only one border radius: 2px.** This is editorial sharpness. No `12px` rounded cards. No `999px` pills.
- **Borders, not shadows.** There are no box-shadows in the design system. If something needs to pop, it uses `var(--bg-elev)` (darker surface) or `var(--line-strong)` (brighter border).
- **1px lines everywhere.** Dividers, card borders, form rows. Heavy uses `var(--line-strong)`.
- **One decorative gradient.** The `.monogram::after` radial. That's it. Do not add more.
- **No blobs, no SVG dividers, no decorative icons.** Anything decorative has to earn its pixels.

## The mono-glyph vocabulary

Thesis rows use ASCII-style geometric markers to categorize:

- `▲` — technology / upward / signal
- `◇` — rare / hard-tech / crystalline
- `●` — concrete / grounded / fintech

These markers **stand in for illustrated icons**. Never replace them with emoji (🚀, 💎, 💰), Phosphor icons, or Lucide icons. The whole point is that the site doesn't use icon sets.

If you add a new thesis, pick a mono glyph that extends this vocabulary. Candidates: `◆` (solid diamond), `○` (open circle), `▽` (down triangle), `■` (solid square), `◐` (half-filled circle). Never colored, never filled with gradient.

## Motion

- **Transition durations:** 200ms (hover/micro), 300ms (theme/color), 600–700ms (reveal-on-scroll).
- **Easing:** `cubic-bezier(.2, .8, .2, 1)` — quick out, slow settle. Used for all custom transitions.
- **Reveal animation:** fade + 8–10px translateY. Staggered by 70ms between siblings (up to 6).
- **`prefers-reduced-motion: reduce`** is honored. All reveals snap to `.in`, the status dot stops pulsing, the caret stops blinking.

## Components

| Selector | Role |
|---|---|
| `.btn` / `.btn-primary` | Button system (mono label, 2px radius, hover translate) |
| `.tag` | Inline categorical label (used in thesis tags, avg-reply badges) |
| `.chip` / `.chip.on` | Segmented single-select (form role/sector, audience switch) |
| `.section-head` | Mono label row: num + title + rule |
| `.section-lede` | Bold editorial statement that follows `.section-head` |
| `.audience-switch` | Segmented control for founder/VC/both filtering |
| `.audience-bar` | Top-of-page audience selector that reflows sections |
| `.thesis-row` | Full-width editorial row in Thesis section |
| `.pitch-step` | Numbered timeline row in Pitch section |
| `.dd-list` | Do-send / don't-send bullet list (green + / red –) |
| `.vc-wrap` | Dedicated card for Partners section |
| `.note` / `.note.draft` | Notes list row (anchor or dimmed div) |
| `.form-row` / `.form-row.invalid` | Labeled form field, red state |
| `.form-success` | Post-submit success block with mailto fallback |

### Component rules of thumb

- **Cards only when the card IS the interaction.** Do not wrap arbitrary content in a box for decoration. Thesis used to be cards; it's now prose rows because the card shape was doing nothing.
- **Form labels are mono.** Inputs are sans. This reinforces label = structure, input = content.
- **CTAs are buttons; navigation is underlined hover.** Never style a plain link like a button unless it's a primary action.

## Audience routing

The page has two primary audiences (founders, VCs). The `[data-audience]` attribute on `<html>` controls:

1. Whole-section show/hide via `[data-aud-only="..."]` attributes on `<section>` elements (Pitch = founders-only, Partners = vcs-only).
2. Inline content swaps via `[data-for="..."]` attributes (contact heading and sub-copy).
3. Top nav filtering (hides the link to any hidden section).

Values:
- `founders` — primary audience. Sees Hero, Thesis, Pitch, Notes, Contact.
- `vcs` — secondary. Sees Hero, Thesis, Partners, Notes, Contact.
- `both` — default first-visit. Sees everything. Contact card shows the founder-variant heading.

Persistence: selection saved to `localStorage['kq:audience']`.

## Accessibility baseline

These are load-bearing, not decorative. Don't remove them:

- Skip link (`.skip-link`) that reveals on focus.
- Visible `:focus-visible` outlines using `--accent`.
- `aria-pressed` on audience-switch buttons, `role="radiogroup"` on chip rows.
- `aria-label` on decorative `.monogram`, the stats sidebar, and the audience bar.
- `inputmode="email"` and `autocomplete` hints on all form fields.
- Color-coded bullets for do/don't also carry text marks (`+` / `–`) — colorblind-safe.
- `prefers-reduced-motion` honored for every animation.
- `<noscript>` on original notes list — now not needed since notes are static HTML.
- Touch targets: all chips and buttons are ≥ 32px tall; audience switch buttons are 28px (acceptable for inline secondary control, but push to 44px if possible).

Run the basics before shipping: 4.5:1 contrast on body text, 3:1 on muted labels and UI controls, keyboard-only navigation from hero to contact.

## Responsive

One breakpoint: `820px`.

Above 820px: full grids (3-col thesis rows, 2-col pitch, 2-col contact, hero with stats sidebar).
At/below 820px: single-column stacks. Navigation in topbar hides entirely — the sticky "Get in touch" chip replaces it. Consider adding a hamburger if the nav gets longer.

## Things that do NOT belong here

A running list of patterns that would pull the design toward SaaS slop. **Do not add:**

- Purple / indigo / blue-purple gradients anywhere, ever.
- Icon-in-colored-circle thumbnails.
- 3-column feature grids with symmetric cards.
- Centered hero text, centered section heads.
- Decorative illustrations of rockets, AI brains, abstract waves.
- Testimonial carousels.
- Stock photography.
- Rounded pill CTAs.
- Emoji as bullet points or icons in body copy.
- "Trusted by" logo strips (unless the scout-program funds explicitly want the attribution).
- Generic hero copy ("Welcome to my world", "Unlock the power of venture", etc.).
