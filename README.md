# AI Exam Prep

BCSE306L Artificial Intelligence: module priorities (M1–M7) and FAT question papers (B1, D1, D2, E1, E2), with a View mode for reading and a Study mode for tracking progress.

Plain HTML, CSS and JavaScript (ES modules). No framework, no build step, no runtime dependencies.

## Layout

```
public/            the site (this is what gets deployed)
  index.html
  css/styles.css
  js/app.js        rendering, routing, modes, theme, tab animation
  js/api.js        loads data/*.json
  data/            modules.json, papers.json
  sw.js            service worker: instant repeat visits, works offline
scripts/
  dev-server.js    local static server
  check.js         validates data and file references
vercel.json        static deploy + cache headers
```

## Run locally

```bash
npm start      # http://localhost:3000
npm test       # sanity checks
```

## Deploy

Vercel picks up `vercel.json` and serves `public/` as a static site. Any static host works (GitHub Pages, Netlify, Cloudflare Pages) by pointing it at `public/`.

## Why it is fast

- Static files on a CDN: no server or API call between the visitor and the content.
- The theme and mode are applied before first paint, so nothing flashes.
- The scripts and data are preloaded in parallel with the page.
- A service worker serves repeat visits from cache and refreshes in the background. After changing a file in `public/`, bump `VERSION` in `public/sw.js`.

## Editing content

Edit `public/data/modules.json` and `public/data/papers.json`, run `npm test`, then commit.
