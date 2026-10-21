# Do Tell Gallery

**▶ Live demo: https://j0selu1gi.github.io/Art-Gallery-CRM/**

A gallery-management dashboard for the Do Tell gallery: the current show at a glance,
artist rosters, artworks, exhibitions, and a rolling six-month plan of openings —
including DoDoFridays and solo-show slots. Data is edited in place through slide-in
drawers; everything stays in sync with the gallery's records.

Built as a widget for the [Kimi Work](https://www.kimi.com/) dashboard; it also runs
standalone in any browser (see *Running it* below).

## What it does, in plain terms

- **Overview tab** — the gallery at a glance: what's on now, what's next, upcoming
  opening dates, and sales / commission numbers for the current year.
- **Artists tab** — every artist the gallery works with: bio, location, contact
  details, Instagram, website, and the mediums they work in. Add, edit, or remove
  artists from the same screen.
- **Artworks tab** — the catalog: each piece linked to its artist, with medium,
  dimensions, year, and price.
- **Exhibitions tab** — past and upcoming shows: which artist, which artworks, dates,
  and whether it's a solo show, a curated group show, or a DoDoFriday.
- **Planning tab** — a six-month look-ahead calendar built around the gallery's real
  rhythm: second Saturdays (DoDoFridays) and fourth Saturdays (solo openings). Open
  slots, proposed shows, and confirmed shows are color-coded so you can see gaps at a
  glance.
- **Money logic** — sales are tracked with the gallery's standard 30% commission, so
  the overview can show both gross sales and the gallery's share.

## How it works (technical, but simple)

- **One file, no build step.** All markup, styles, and logic live in `index.html`.
- **Data.** Four collections — `artists`, `artworks`, `exhibitions`, and `plans`
  (monthly plan entries) — are normalized on load. Inside Kimi Work the widget reads
  live data from its bound data slot (synced from the gallery app's own state file);
  standalone, it uses the rich sample dataset embedded in the file (`FALLBACK`).
- **Editing.** A single slide-in drawer component handles every record type: it builds
  a form from a per-kind field schema, and on Save emits the change back through the
  widget host (`window.DaimonWidget.emit`) so the rest of the gallery system stays in
  sync. Standalone, edits apply to the in-memory copy for the session.
- **Date math.** Opening dates aren't stored by hand — the app computes the first,
  second, and fourth Saturdays of each month, so the schedule always follows the real
  calendar.
- **Generated covers.** Exhibitions without a photo get a deterministic abstract SVG
  cover, generated from a seeded random generator based on the exhibition's id — same
  show, same cover, every time, with no image assets to manage.
- **Theming.** Uses Kimi's design tokens (CSS custom properties); `kimi-standalone.css`
  supplies equivalent values outside Kimi Work.

## Running it

- **In Kimi Work:** place `index.html` in a Widget workspace and bind a data slot for
  live sync.
- **Standalone:** open `index.html` in a browser. The embedded sample dataset is used
  automatically.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app (UI + logic + embedded sample data) |
| `kimi-standalone.css` | Fallback theme/variables for standalone use |

## A note on the sample data

The embedded dataset is based on the gallery's real working records, but personal
contact details (email addresses and phone numbers) have been removed before
publication. If you fork this for your own gallery, replace the sample records with
your own data.

## License

MIT — free to use, copy, modify, and share. See [LICENSE](LICENSE).
