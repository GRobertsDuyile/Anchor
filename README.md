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

Everything lives in `index.html`. The parts worth knowing:

- `WEEKLY` — the seven-day template of fixed blocks and training.
- `DOMAINS` — suggestion libraries per domain, each with a full and a minimum
  variant.
- `getDayTimeline(dow)` — paints a 1440-minute array and collapses it into
  segments; this is where block overlaps resolve.
- `generateSuggestions(remaining, minDay, dow)` — fits activities into the time
  left before the next segment starts.

## Known issue: persistence

Saving runs through `window.storage`, which exists in the Claude artifact preview
and nowhere else. Opened as a plain file or served from static hosting, every
call to `loadKey` and `saveKey` fails. Both are wrapped in `try`/`catch`, so the
failure is silent: onboarding appears to save, reflections appear to record, and
nothing survives a reload.

This is a decision rather than a patch, and it has not been made yet. Either
swap in a runtime state capability, or use guarded `localStorage` and accept
that data stays on one device. Do not deploy the file as it stands.

## Status

Paused mid-build. See the persistence issue above before adding features.
