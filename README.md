# Slotbook

An FFCS timetable planner for VIT, Winter Semester 2026–27.

**Live site:** https://suyasht21.github.io/slotbook/

## What it does

**Slot View**
- The full Monday–Friday grid from 8:00 AM to 7:20 PM, drawn to the minute (each tick is 10 minutes).
- Click a theory or lab slot to see where it lands. Slots that would clash with your picks lock themselves.
- Shows your theory classes per week and lab count, plus a copyable slot string like `A1+TA1+L33+L34`.

**Timetable Planner**
1. Pick a course from Discipline Core, Discipline Elective or Open Elective.
2. Choose **one faculty**. All of that faculty's theory slots and matching labs are tried.
3. Courses that clash with ones you already added can't be added. The page names the clashing slots and the course that took them.
4. Browse every clash-free timetable. Filter by morning, evening or mixed theory, and sort by your course order, fewest 8 AM starts, or least time on campus.

A new visitor starts with an empty planner. Everything you do is saved in your browser: your courses, the course you have open, your Slot View picks, filters and the timetable you were looking at. Reloading or coming back later picks up where you left off. Saves stay on that browser and device only.

Visits are counted with [GoatCounter](https://www.goatcounter.com), which uses no cookies and collects no personal data.

## Slot rules used

| Pattern | Classes a week |
|---|---|
| `A1` | 2 |
| `A1+TA1` | 3 |
| `A1+TA1+TAA1` | 4 |
| `L1+L2` | one 1h 40m lab |

- Theory classes are 50 minutes, starting on the hour: 8–12 in the morning, 2–6 in the evening.
- Labs are two 50-minute periods back to back: 8:00, 9:50, 11:40, 2:00, 3:50 and 5:40.
- Wednesday has no morning theory after 10:50 (extramural hours), but all labs still run.
- A course's theory and lab must be taken with the same faculty. Morning theory pairs with an afternoon lab (L31–L60), and evening theory pairs with a morning lab (L1–L30).
- Two slots clash only if their times overlap on the same day. One ending exactly when the other starts is fine.

## Updating course data

Everything lives in `index.html`. Courses are in the `RAW` array inside the script. Each course lists its theory and lab sections as `[slot, venue, faculty]`:

```js
{ id: 'BEEE303', cat: 'DC', kind: 'TH', name: 'Control Systems', codes: ['BEEE303L', 'BEEE303P'], labTitle: 'Control Systems Lab',
  theory: [['G1+TG1', 'TT104', 'JANAKI M']],
  labs: [['L33+L34', 'TT045', 'JANAKI M']] },
```

`kind` is `TH` (theory, with an optional separate lab code), `ETH` (embedded theory + lab), `LO` (lab only) or `SS` (soft skill). `cat` is `DC`, `DE` or `OE`.

## Deploying

The site is a single static `index.html` with no build step. It's served by GitHub Pages from the `main` branch root, so every push to `main` redeploys it.

To turn it on: repo **Settings → Pages → Build and deployment**, set Source to **Deploy from a branch**, then pick `main` and `/ (root)`.

Always double-check slots on VTOP before you register.
