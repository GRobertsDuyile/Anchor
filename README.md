# Anchor

A single-file personal day-planning webapp. The day is modelled relative to wake
time rather than the clock, so every suggestion is sized to the gap that is
actually left in front of you.

## Running it

Open `index.html` in a browser, or serve the folder:

```
python3 -m http.server 8000
```

No build step, no dependencies, no package manager.

Service workers require `http://` or `https://` — opening `index.html` directly
as a `file://` URL will run the app fine but skip offline caching and the
install prompt. Serve it locally (as above) or from any static host (GitHub
Pages, Netlify, etc.) to test the actual "Add to Home Screen" install.

## What it does

Onboarding captures wake time, sleep target, work hours and morning faith
minutes, together with a priority order across study, family and faith and a set
of editable fixed weekly blocks.

Three tabs run off that profile:

- **Today** — a hero card naming the current segment and suggesting what fits
  the remaining time, with a reshuffle control and a minimum-day toggle; plus a
  bedtime card, a day-shape bar, a seven-day reflection strip and a four-domain
  check-in.
- **Week** — the per-day timeline, with fixed blocks editable per day.
- **Food** — a static reference list.

## Structure

- `index.html` — the app itself.
- `manifest.json` — PWA manifest (name, theme colour, icons) for "Add to Home Screen."
- `service-worker.js` — cache-first app-shell caching for offline load. Bump `CACHE_NAME` inside it on any deploy that changes `index.html`, the manifest, or the icons.
- `icon-192.png`, `icon-512.png` — home-screen icons.

Inside `index.html`, the parts worth knowing:

- `WEEKLY` — the seven-day template of fixed blocks and training.
- `DOMAINS` — suggestion libraries per domain, each with a full and a minimum variant.
- `getDayTimeline(dow)` — paints a 1440-minute array and collapses it into segments; this is where block overlaps resolve, including the per-day work-end override below.
- `generateSuggestions(remaining, minDay, dow)` — fits activities into the time left before the next segment starts.

## Persistence

Saving runs through IndexedDB (`loadKey`/`saveKey`, store `anchor-db`), wrapped
in `try`/`catch` so a storage-disabled context degrades to in-memory-only
rather than throwing. This works standalone, served from static hosting, or
installed on a phone as a PWA.

It does not sync across devices — that's what **Export/Import** (in Setup) is
for: export writes a single JSON file with everything (profile, weekly blocks,
work overrides, reflections, minimum-day flags); import reads one back in.
That file is the actual portable copy of your data — back it up, move it to
another device, or keep it before clearing browser storage. If real
cross-device sync is ever needed, a small backend is the next step; it isn't
required for single-device personal use.

## Per-day work end

Each weekday has a **"Leave work by"** time in Setup, so a fixed block late in the
afternoon can shorten the work segment on that day only. `getDayTimeline` uses
this per-day value instead of a flat end time, so the Today and Week views show
accurate "at work until" times.

## Status

Persistence, offline install, and the per-day work end are resolved.
Next candidates: a lunch-hour or mid-day study gap for the researcher role
(currently there's no attempt to model gaps between meetings within the work
block), and letting weekend chores have an editable start time instead of the
current 09:00 guess.
