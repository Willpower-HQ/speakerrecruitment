# speakerrecruitment

Willpower's speaker recruitment landing page — "Take the stage the category-defining brands trust."

## Files

- `index.html` — the landing page (a Claude Design component: hero, three series, why-speak, event films, past-speaker directory, vetting, apply).
- `support.js` — the Design runtime that renders the page. Loads React from a CDN and self-boots. `index.html` must be served alongside it.
- `.nojekyll` — tells GitHub Pages to serve files verbatim.

## Running locally

Serve the folder over HTTP (the runtime re-fetches the page, so `file://` won't fully work):

```
python3 -m http.server 8000
# open http://localhost:8000/
```
