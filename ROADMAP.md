# Roadmap

Anchor began as a planner for one person's week. The work below turns it into a planner anyone can set up, then extends it.

## 1. Anyone can set it up

- Replace the built-in sample week with a five-step setup: your day, your work, your priorities, your fixed blocks, and a review.
- Let users name up to four priorities of their own, in their own order.
- Let one fixed block repeat on several days.
- Offer a clearly labelled sample week for first-time visitors.
- Replace the Food tab with a Notes tab the user writes.
- Store data with a version number, and convert older backups automatically on import.
- Serve the fonts from this repository, so the app makes no requests to other sites.

### Bugs to fix in this stage

- "Show a different mix" permanently reorders your saved priorities. It should change only the current suggestions.
- Check-ins made between midnight and 1am in summer time are saved under the previous day.
- The wind-down message assumes a 5:30 wake time.

## 2. Tests

- Move the planning logic into its own file so it can be tested without a browser.
- Add tests for the timeline, the suggestions and the backup conversion, using Node's built-in test runner.
- Run the tests on every push with GitHub Actions.

## 3. Accessibility

- Make every tab and button reachable by keyboard.
- Link every form label to its field.
- Give the check-in dots and the day-shape bar a text equivalent.
- Meet WCAG 2.2 level AA throughout.

## 4. First release

- Deploy to GitHub Pages and test installing on Android and iPhone.
- Add a maskable icon with safe padding.
- Tag version 1.0.0.

## 5. After the first release

- Model gaps inside working hours, such as a lunch break.
- Make the weekend start time editable.
- Import and export fixed blocks as calendar (.ics) files.
- A short weekly review built from the reflection strip.
- Move interface text into one file so Anchor can be translated.
- Reminders that fire while the app is closed. This needs a decision, because a web app with no server cannot schedule them reliably.

## Out of scope

These would break Anchor's design, so they are not planned:

- Accounts, cloud sync or any server that stores your data.
- Analytics, tracking or advertising.
- Streaks, scores or anything designed to pressure you into opening the app.
