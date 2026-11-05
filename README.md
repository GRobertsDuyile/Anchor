# Anchor

Anchor is a day planner that works from your wake time rather than the clock. It knows what is fixed in your week, so at any moment it can suggest what fits in the time actually left before your next commitment.

## Who it is for

Anchor is for people whose days are shaped by commitments they cannot move, such as school runs, shifts, classes or training, and who want help using the gaps between them. It suits anyone who has found that a to-do list ignores how much time is really left.

## What it does

Setup asks for your wake time, sleep target, working hours, time each morning for faith and prayer, the order of your priorities, and the fixed blocks in your week. Anchor ships with a sample week so you can see it working straight away; change any of it in Setup.

**Today** names the segment you are in and suggests what fits the time remaining, drawn from your priorities in order. You can ask for a different mix, or switch to a minimum day when you have less to give. Below sit a bedtime card, a bar showing the shape of the day, a seven-day reflection strip and an evening check-in.

**Week** shows each day as a timeline.

**Food** is a short reference list. It will become a notes tab you write yourself (see the roadmap).

## Your data stays on your device

There is no server, no account and no analytics. Everything you enter is stored in your browser using IndexedDB. **Export backup** in Setup saves it all to one JSON file, and **Import backup** reads it back on the same or another device.

One exception for now: the page loads its two fonts from Google Fonts. Serving them from this repository instead is the first item on the roadmap.

## Running it

Open `index.html` in a browser, or serve the folder:

```
python3 -m http.server 8000
```

Then open http://localhost:8000. There is no build step and nothing to install. Opening the file directly works, but the browser then skips offline caching and the install prompt, so serve it, locally or from a static host such as GitHub Pages, to test installing it as an app.

## Built with

Plain HTML, CSS and JavaScript, with no framework and no dependencies. A service worker caches the app for offline use, and a web app manifest makes it installable on a phone.

## Structure

- `index.html`: the app.
- `manifest.json`: name, theme colour and icons for installing.
- `service-worker.js`: offline caching. Bump `CACHE_NAME` on any deploy that changes the cached files.
- `icon-192.png`, `icon-512.png`: home-screen icons.

Inside `index.html`:

- `WEEKLY`: the sample week of fixed blocks and training.
- `DOMAINS`: suggestions for each priority, each with a full and a minimum version.
- `getDayTimeline(dow)`: lays the day out minute by minute, resolves overlaps between work and fixed blocks, including each day's "Leave work by" time, and returns the day as segments.
- `generateSuggestions(remaining, minDay, dow)`: fits suggestions into the minutes left before the next segment.

## Roadmap

See [ROADMAP.md](ROADMAP.md).

## Licence

[MIT](LICENSE)
