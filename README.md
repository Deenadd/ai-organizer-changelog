# AI Organizer — Changelog

The public changelog for the AI Organizer iOS app. A static site: `index.html` renders
`changelog.json`, nothing to build, nothing to install. Vercel deploys it on every push to `main`.

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
  "added": ["…"],
  "improved": ["…"],
  "fixed": ["…"]
}
```

- `version` / `build` match `MARKETING_VERSION` / `CURRENT_PROJECT_VERSION` in the app's `project.yml`.
- `date` and `time` are when the build went to TestFlight, in India Standard Time.
- Any of `added` / `improved` / `fixed` may be omitted or empty; the section simply doesn't render.
- Write for the person using the app, not from the commit log: what they'll notice, in their words.

Then commit and push. The site updates within about a minute.
