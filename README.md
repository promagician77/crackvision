# Crack Metrology Bench

A single static page. No build step, no dependencies, no framework — one
`index.html` with inline CSS and JS, plus Google Fonts over the network.

## What it shows

A synthetic crack with a **known true width profile**, used as a test object.
Because the truth is known, two measurement methods can be scored against it
rather than against each other:

- **binary mask** — width quantises to whole pixels, so its error is bounded
  below by the ground sample distance
- **sub-pixel** — partial-area estimation off the probability map, which keeps
  resolving below one pixel until the signal itself is gone

Drag the GSD slider on the Aperture tab. As it coarsens, the binary mask first
mis-sizes cracks, then puts them on the wrong side of the ACI-318 0.30 mm
reporting line, then stops seeing them at all.

Five tabs: Aperture, Tiling, Confusables, Output, Datasets.

No figure on the page is a claim about any real inspection system.

## Run locally

```bash
npm run dev          # http://localhost:3000
```

Or just open `index.html` in a browser — it is self-contained.

## Deploy

**Vercel CLI**

```bash
npm i -g vercel
vercel          # preview deployment
vercel --prod   # production
```

Framework preset: **Other**. Build command: none. Output directory: `.` (root).

**Via Git**

Push this directory as a repository, then import it at
[vercel.com/new](https://vercel.com/new). Vercel detects a static site and
serves `index.html` with no configuration beyond the `vercel.json` here.

## Notes

- `vercel.json` sets security headers and disables caching on the HTML so a
  redeploy is visible immediately.
- `<meta name="robots" content="noindex">` keeps the page out of search results.
  Remove it if you want it indexed.
- Theme preference is stored in `localStorage`, scoped to the deployed origin.
- The clipboard copy buttons need HTTPS, which Vercel provides. Over plain
  `http://localhost` they fall back to selecting the text.
