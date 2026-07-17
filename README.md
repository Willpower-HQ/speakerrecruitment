# Speaker Recruitment

Willpower's speaker recruitment landing page: *"Take the stage the category-defining brands trust."*

An invitation page for prospective speakers, showcasing the room, past events, the past-speaker directory, and the vetting standard.

**Live:** https://willpower-hq.github.io/speakerrecruitment/

## Sections

| Section | What it shows |
|---|---|
| Hero | Video backdrop, headline, and live-counting stat cards |
| The Room | The three curated series (Wellness House, Catalyst, World of Sports) |
| Why Speak | Expandable benefit cards |
| Watch the Room | Past-event films, filterable by series, with a YouTube modal |
| Past Speakers | Verified past-speaker directory with per-speaker detail views |
| Vetting | The vetting standard |
| Apply | The "you're invited" call to action |

## Files

| File | Purpose |
|---|---|
| `index.html` | The landing page. A Claude Design component (an `x-dc` template plus a logic class). |
| `support.js` | The Design runtime. Parses the template, loads React from a CDN, and boots the page. |
| `.nojekyll` | Tells GitHub Pages to serve the files verbatim (no Jekyll processing). |

`index.html` and `support.js` must stay together in the same folder. The runtime is a separate file on purpose: `support.js` contains literal `<x-dc>` markers in its own source, so inlining it into the HTML breaks the runtime's self-parse.

## Running locally

The runtime re-fetches the page over the network, so open it through a web server, not straight from disk (`file://` will not fully work).

```bash
python3 -m http.server 8000
# then open http://localhost:8000/
```

## Editing content

### Add or edit a past speaker

Speakers live in the `speakers` array inside `renderVals()` in the logic class at the bottom of `index.html`. Search for `const speakers = [` and append an entry:

```js
{
  name: 'Full Name',
  title: 'Role · Company',       // e.g. 'Founder & CEO · Tiny Health'
  brand: 'Company',              // short label on the card and chip
  img: P + 'speaker-first-last.jpg',
  g1: P + '<event-photo>.jpg',   // two supporting event photos for the detail view
  g2: P + '<event-photo>.jpg',
  spoke: 'Short talk topic',
  bio: 'Two-sentence background.',
  idx: N,                        // sequential, 0-based
  delay: 0                       // reveal stagger: 0 / 70 / 140 / 210 per row of 4
}
```

`P` is the photo host base (`https://willpowerhq.com/assets/photos/`). Reuse an existing event photo for `g1` / `g2` from the pool already in the file.

### Headshots

Headshots must be licensed images that Willpower owns. Do not embed press or LinkedIn photos. Upload a headshot to the photo host as `speaker-first-last.jpg` and point `img` at it.

## Deployment

Hosted on GitHub Pages from the `main` branch, root folder. Any push to `main` redeploys automatically. No build step.

## Known issues

- Some headshots at `willpowerhq.com/assets/photos/speaker-*.jpg` currently return 404, so those cards show no photo. Event photos load fine. Uploading the missing headshots fills the cards in with no code change.
