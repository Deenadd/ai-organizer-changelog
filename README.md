# AI Organizer — Changelog

The public changelog for the AI Organizer iOS app. A static site: `index.html` renders
`changelog.json`, nothing to build, nothing to install. Vercel deploys it on every push to `main`.

## Pages

- `/` — the latest year: “What’s new”, a month timeline with a mark on each build’s day, and one row per build.
- `/2026` — a specific year (year links appear above the timeline once there is more than one year).
- `/2026/<slug>` — one build’s full notes. The slug is derived from the title
  (or set `slug` on the entry to pin it). `vercel.json` rewrites these paths to `index.html`.

## The icon

`favicon.ico` and `icon-*.png` are the app's own icon
(`AIOrganizer/Resources/Assets.xcassets/AppIcon.appiconset/icon-1024.png`), masked to the iOS
squircle so the corners are transparent in a browser tab. `apple-touch-icon.png` stays square and
opaque, because iOS applies its own mask and renders transparency on black. Regenerate all of them
from the source icon whenever the app's icon changes.

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
