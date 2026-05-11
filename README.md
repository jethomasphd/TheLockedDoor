# Codex of the Flood — Volume II

**The Flood &amp; the Locked Door**
*A liturgy for the bottleneck generation.*

By Jacob E. Thomas, PhD · JEThomasPhD@gmail.com
Dedicated to Meridian.

---

## What this is

A self-contained, single-file HTML codex (`index.html`) with six archival plates and a `favicon.svg`. All paths are relative; the directory deploys to any static host without modification.

## Quick deploy

This is a static site. Drop the entire directory onto any of these and it works immediately:

- **GitHub Pages** — push to a repo, enable Pages, point at the branch root
- **Cloudflare Pages** — connect the repo or upload via Wrangler
- **Netlify** — drag the folder into the Netlify drop zone
- **Vercel** — `vercel deploy`
- **Any web server** — copy the directory to your document root

No build step. No dependencies to install. The codex pulls Chart.js from a CDN (jsDelivr) and Google Fonts (Cormorant Garamond, EB Garamond, IBM Plex Mono).

## File inventory

```
codex-of-the-flood/
├── index.html              ← the codex (3,300 lines, self-contained)
├── favicon.svg             ← ember sigil, 32×32
├── Cover_Plate.png/.webp   ← Plate VII — The Gate (Porta Aeterna)
├── The_Vault.png/.webp     ← Plate I — The Vault
├── The_Tempo.png/.webp     ← Plate II — The Tempo (Sodium Light / Rising Water)
├── The_Held_Throne.png/.webp ← Plate III — The Held Throne
├── The_Elegy.png/.webp     ← Plate IV — The Elegy
├── The_Ark.png/.webp       ← Plate V — The Ark (Five Pillars)
├── CODEX_CHANGES.md        ← changelog for the v4 elevation pass
├── TEXT_NOTES.md           ← observations only, no edits
└── README.md               ← you are here
```

Each plate ships in two formats. The HTML uses `<picture>` to serve WebP to supporting browsers and falls back to PNG everywhere else. Don't delete either; both are needed.

## After deploying

1. **Update the canonical Open Graph URL.** The HTML uses relative paths for `og:image`, which works for sharing inside most platforms but some require absolute URLs. Once you know the production URL, find these lines near the top of `index.html`:

   ```html
   <meta property="og:image" content="./Cover_Plate.png">
   <meta name="twitter:image" content="./Cover_Plate.png">
   ```

   Replace with the absolute URL:

   ```html
   <meta property="og:image" content="https://your-domain.com/Cover_Plate.png">
   <meta name="twitter:image" content="https://your-domain.com/Cover_Plate.png">
   ```

   Also add a `<link rel="canonical" href="https://your-domain.com/">` if you want clean SEO.

2. **Verify Lighthouse.** Open Chrome DevTools → Lighthouse. Target scores: Performance ≥ 88 mobile / ≥ 95 desktop, Accessibility ≥ 95, Best Practices ≥ 95.

3. **Smoke test the experience.** Read it once on desktop, once on mobile. The intended cinematic flow:
   - Gate dismisses → Cover Plate full-bleed passage fades up
   - Codex header rises from beneath the cover gradient
   - Fragments I–IX, each with its own plate where applicable
   - Sigil interludes between fragments not separated by a Spiral
   - Three Spiral summonings — each speech reveals line-by-line
   - The Widow Elegy with The_Elegy plate before the verdict
   - The Ark frieze (The_Ark) as frontispiece to the Five Pillars manifest
   - The Prayer, line by line
   - Marginalia with all 16 sources

## Browser support

Tested patterns: Chrome / Edge / Safari / Firefox current. The codex degrades gracefully:

- `backdrop-filter` (used on tooltips) falls back to opaque dark backgrounds in browsers without support.
- `prefers-reduced-motion: reduce` short-circuits all animation. Ken Burns plate zooms, sepia lifts, gold flecks, scroll reveals, Spiral line-by-line, number counter, prayer stagger — all become instant or static.
- `prefers-color-scheme: light` is deliberately ignored. The codex is dark by liturgical intent.
- Print stylesheet collapses everything to grayscale with page breaks per fragment, preserving all citations and prose. Try `Cmd+P` / `Ctrl+P` for the archival print form.

## Citing or sharing

If anyone wants to cite this:

> Thomas, J. E. (2026). *The Flood &amp; the Locked Door — A Codex.* (Codex of the Flood, Vol. II.) Available at [your URL].

All factual claims are sourced. The 16 sources are listed in the marginalia section at the end of the codex with clickable anchors from each citation tooltip.

## License / use

No formal license declared. If you encounter this and want to translate, adapt, or remix any of it, please reach out: **JEThomasPhD@gmail.com**. The work is built on public-record data; the framing, voice, and assembly are mine.

---

*The Word against the Flood.*
