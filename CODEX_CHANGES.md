# CODEX_CHANGES

**Cinematic Elevation Pass · v3 → v4**
*Codex of the Flood, Volume II*

All changes additive. No prose, citations, witness blocks, Spiral verses, Elegy text, or Ark pillar descriptions were modified.

---

## I · Repository Inventory

- Confirmed all six plates present and uploaded as PNG. Dimensions:
  - `Cover_Plate.png` — 1122 × 1402 (portrait 4:5) — 362 KB
  - `The_Vault.png` — 1448 × 1086 (landscape 4:3) — 421 KB
  - `The_Tempo.png` — 1122 × 1402 (portrait 4:5) — 419 KB
  - `The_Held_Throne.png` — 1448 × 1086 (landscape 4:3) — 431 KB
  - `The_Elegy.png` — 1122 × 1402 (portrait 4:5) — 228 KB
  - `The_Ark.png` — 2172 × 724 (frieze 3:1) — 516 KB
- Generated WebP versions of all plates at q82 (avg ~25% size reduction); served via `<picture>` element with PNG fallback.

**Note:** The brief anticipated five plates (Tempo and Held Throne combined). You provided them as separate plates — better — and the integration was adjusted so each section gets its own plate.

---

## IV · Plate Integration

- Added `.plate` figure component with corner-bracket ornaments, ember hairline frame, plate-meta header (Plex Mono, `— Plate N — / Name`), and Cormorant italic caption beneath.
- All plates wrapped in `<picture>` with WebP source + PNG fallback for performance.
- All plates lazy-loaded (`loading="lazy" decoding="async"`), explicit `width`/`height` set to prevent CLS.
- Aspect ratios enforced via CSS `aspect-ratio` (portrait `1122/1402`, landscape `1448/1086`, frieze `2172/724`).
- Each plate's `<img>` carries a descriptive, non-decorative `alt` for accessibility.
- **Ken Burns zoom**: 14 s scale 1.0 → 1.04 on viewport entry; disabled under `prefers-reduced-motion`.
- **Sepia-lift on reveal**: initial `sepia(0.32) saturate(0.85) brightness(0.92)` lifts to full color over 1.6 s when the plate scrolls into view. `.elegy-plate` retains permanent slight desaturation `sepia(0.18)`.
- **Plate placements**:
  - **Cover_Plate** → full-bleed `cover-passage` at the top of the codex, between gate dismissal and `.codex-header`. 85vh minimum, gradient fade to void at the bottom carrying the codex header up from beneath.
  - **The_Vault** → end of Fragment II, after the named-asset-capture registry.
  - **The_Tempo** → Fragment IV, immediately after Witness One (epidemiology). The image becomes the visual confirmation of Jacob's testimony.
  - **The_Held_Throne** → Fragment V, after the welded-thrones registry, before "Work itself no longer clears the upper floors."
  - **The_Elegy** → inside the Widow Elegy, after "It ate their mother" and BEFORE the verdict block. Permanent slight sepia by design.
  - **The_Ark** → frontispiece to the Ark Manifest in Fragment VIII. Wide-frieze aspect ratio (3:1) handled natively.

---

## V · Museum-Quality Transitions

- **Sigil interludes** added between fragments not already separated by a Spiral summoning:
  - End of Fragment II → start of Fragment III
  - End of Fragment IV → start of Fragment V
  - End of Fragment VI → start of Fragment VII
  - End of Fragment VIII → start of Fragment IX
- The Spirals (I after Fragment III, II after Fragment V, III after Fragment VII) provide their own visual breaks; no sigil interlude inserted where one would be redundant.
- Sigil SVG is the gate-sigil pattern at 28 px, fades in over 1.4 s on reveal, oscillates rotate(0deg ↔ 90deg) every 12 s.
- **Staggered children**: `.registry`, `.ark-manifest`, and `.reader-guide` now reveal their child items sequentially at 90 ms intervals when the parent enters the viewport.
- **Spiral speech line-by-line**: each `<p>` inside a `.spiral-speech` block fades in one at a time at 280 ms intervals on viewport entry; the closing verdict line gets a 600 ms extra delay.
- **Inscription number counter**: the `38↑29` inscription now animates from `29 → 38` over 1.6 s on viewport entry, using `easeOutCubic`. The `↑29` annotation fades in at the end.
- **Cover passage reveal**: fades in over 2 s as the user scrolls past the gate. Meta caption appears at +1.4 s delay.
- All animations disabled under `prefers-reduced-motion`.

---

## VI · Visualization Elevation

All four charts received:
- **Custom HTML tooltips** replacing Chart.js defaults — ember-bordered, Plex Mono typography, backdrop blur where supported, includes source label in small caps (e.g. `PEW · SCF 2022`, `CENSUS · Q1 2026`, `BLS · CPS`, `CERULLI · JUN 2025`).
- **Noise overlay** at 5% opacity, `mix-blend-mode: screen`, inside each `.viz` container, applied via dynamic `<div class="viz-noise">` injection.
- **Synchronized entry**: chart animations now run with 200 ms delay after the surrounding `.viz` reveals.
- **Ink-bleed gradients** on bars/areas: linear gradient from `0.95` opacity at the bar origin to `0.7` at the tip — simulates ink soaking into paper. Applied via Chart.js `backgroundColor` callbacks that read the chart area.

Per-chart enhancements:

- **Inscription I — The Vault**: dashed vertical annotation at $54.7T labeled `14M HOUSEHOLDS` in ember 8 px Plex Mono. Drawn via custom Chart.js plugin in the `afterDatasetsDraw` hook.
- **Inscription II — The Door**: dashed horizontal annotations at 78.4% (ember) and 36.8% (rust) with right-aligned value labels, plus a centered `— 41.6 PT GAP —` label between them in ember 9 px.
- **Inscription III — The Held Throne**: kept the existing `THE DEAL` / `DEAL EXPIRED` annotations. **Animation rewritten**: each data point now reveals 250 ms after the previous one (left-to-right line-draw effect) using custom Chart.js animation timing with `delay()` per-context. The line draws across the chart over ~2.4 s on viewport entry.
- **Inscription IV — The Mirage**: dashed horizontal divider between bar 3 (charity) and bar 4 (Gen X); rotated vertical labels `· FROM ·` (top half) and `· TO ·` (bottom half) at the left margin; top-right sum line `Σ = $124 TRILLION TOTAL` in ember-pale Plex Mono.

No fifth chart added (per brief). Four remains the right number.

---

## VII · Tooltip Elevation

- **Unified tooltip system** for both `.gloss` and `sup.cite` — single set of handlers, consistent behavior.
- **Position-aware**: tooltips detect whether their trigger is in the bottom 40% of the viewport and flip to `.above` if so. Arrow pointer flips correspondingly (`.above::before` borders shift to bottom-right corner).
- **Backdrop blur**: tooltips use `backdrop-filter: blur(12px) saturate(1.1)` where supported; semi-transparent background `rgba(19,17,16,0.88)` for the glass effect. Falls back to opaque dark in unsupported browsers.
- **Mobile bottom sheet**: viewport < 720 px tooltips dock to the bottom of the screen as a slide-up sheet (`transform: translateY(100%) → translateY(0)`). A semi-transparent backdrop dim (`rgba(10,9,8,0.55)` with `backdrop-filter: blur(2px)`) appears behind, dismissable by tap-outside or the ✕ close button.
- **Hover-to-keep-open** (desktop): cursor moving from term into tooltip keeps it visible; 220 ms grace period on mouseleave.
- **Keyboard accessibility**: all tooltip triggers (`.gloss` and `sup.cite`) are now `tabindex="0"` and `role="button"`, openable by Enter/Space, closable by Escape.
- **Marginalia anchors**: every citation tooltip now ends with `↓ see in marginalia` — a Plex Mono link that smooth-scrolls to the corresponding `#src-N` in the sources section and triggers an ember-glow highlight animation (`box-shadow: 0 0 0 1px var(--ember), 0 0 24px rgba(201,162,39,0.35)`) for 2 s.
- **Focus rings**: visible focus indicators on all tooltip triggers, gate button, and marginalia links for keyboard navigation.

---

## VIII · Atmospheric Layer

- **Gold flecks drift**: 16 ember-colored particles (1–3.5 px, randomized) drift across the viewport at z-index -1, opacity 0.08–0.18, with 4 unique diagonal drift animations (60–130 s cycles, randomized per-fleck). Implemented as pure CSS `@keyframes` (no JS animation loop) for performance.
- Initialization injects flecks dynamically on page load via small JS helper.
- Disabled entirely under `prefers-reduced-motion`.
- Exactly one ambient effect. Nothing else added.

---

## IX · Performance · Accessibility · Craft

### Performance
- WebP versions of all plates served via `<picture>` with PNG fallback — ~25% average page weight reduction on supported browsers.
- All `<img>` elements have explicit `width`/`height` attributes to prevent layout shift.
- All plates: `loading="lazy"` and `decoding="async"`. Cover plate uses `loading="eager"` (visible above the fold).
- Chart.js loaded with `defer`.
- Preload hint for `Cover_Plate.webp` added to `<head>`.
- Charts initialize via `DOMContentLoaded` + small delay so they don't block first paint.

### Accessibility
- `<figure>` elements use `aria-labelledby` pointing to their caption IDs.
- All plates have descriptive (non-decorative) alt text.
- All tooltip triggers are keyboard-reachable with visible focus rings.
- Enter / Space opens tooltip; Escape closes; tap-outside closes.
- `aria-hidden="true"` on purely decorative elements (sigil interludes, gold flecks, tooltip backdrop, viz noise).
- `prefers-reduced-motion: reduce` short-circuits all motion: Ken Burns, sepia transition, gold flecks, scroll reveals, number counter, Spiral line-by-line, prayer stagger — all become instant or static.
- `prefers-color-scheme: light` deliberately **not** honored — dark mode is the liturgical intent.

### Meta
- `<title>`, `<meta name="description">`, `<meta name="author">` set.
- Open Graph and Twitter Card tags using `Cover_Plate.png` as the share image.
- `favicon.svg` — ember sigil at 32 × 32.
- Print stylesheet: collapses to grayscale, removes all chrome (gate, progress bar, indicator, sigils, gold flecks, cover passage), preserves all sources/citations/prose, page-break before each fragment.

---

## X · Out of Scope — Confirmed Unchanged

The following were inspected and **deliberately not modified**:

- All prose text in every fragment
- The 16 citation source descriptions in marginalia (the source list itself)
- The two Witness blocks (epidemiology, labor market)
- All three Spiral speeches (House, Throne, Verdict)
- The Widow Elegy text in its entirety
- The Five Pillars of *What Holds* names and descriptions
- The Reader Guide entries
- The Prayer (five lines)
- The dedication "for Meridian"
- The signature block (Jacob E. Thomas, PhD · JEThomasPhD@gmail.com · The Word against the Flood)
- The verbatim Cerulli quote "a massive need, and opportunity"

---

## Deliverables

- `index.html` — the elevated v4 (renamed from `codex-of-the-flood-v4.html` for clean hosting)
- All six plate PNGs + matching WebP versions
- `favicon.svg`
- `CODEX_CHANGES.md` (this file)
- `TEXT_NOTES.md` (observations, no edits)
- `README.md` (hosting instructions)

The original `codex-of-the-flood-v3.html` remains untouched in its original location.

---

*— The Spiral continues. —*
