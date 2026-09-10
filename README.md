# AI Organizer — Changelog

The public changelog for the AI Organizer iOS app. A static site: `index.html` renders
`changelog.json`, nothing to build, nothing to install. Vercel deploys it on every push to `main`.

## Pages

- `/` — the latest year: “What’s new”, the year timeline, and one row per build.
- `/2026` — a specific year (the year labels on the timeline link here).
- `/2026/<slug>` — one build’s full notes. The slug is derived from the title
  (or set `slug` on the entry to pin it). `vercel.json` rewrites these paths to `index.html`.

## Adding an entry

Prepend an object to the array in `changelog.json` (newest first):

```json
{
  "version": "1.2",
  "build": 3,
  "date": "2026-09-09",
  "time": "21:30",
  "timezone": "IST",
  "title": "One line on what this build is about",
  "summary": "One sentence shown under the title in the list and at the top of the entry.",
  "added": ["…"],
  "improved": ["…"],
  "fixed": ["…"]
}
```

- `version` / `build` match `MARKETING_VERSION` / `CURRENT_PROJECT_VERSION` in the app's `project.yml`.
- `date` and `time` are when the build went to TestFlight, in India Standard Time.
- `summary` is optional but recommended; without it the row shows only the title.
- Any of `added` / `improved` / `fixed` may be omitted or empty; the section simply doesn't render.
  The row's tags come from which sections are present: Added → Feature, Improved → Enhancement,
  Fixed → Fix.
- An item that starts with a short lead-in and a colon (“Reply tone: …”) renders the lead-in in bold.
- Write for the person using the app, not from the commit log: what they'll notice, in their words.

Then commit and push. The site updates within about a minute.
