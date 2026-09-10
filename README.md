# Asheville Beer Choir — Songs from 1985

A retro **1985 Prom** photo album for the Asheville Beer Choir concert — a single-page
static site styled after a vintage "Made in 1985" design (black ground, gold outline
type, the classic sunset rainbow stripe, star/confetti dots). Built to be published on
**GitHub Pages** and reused as a template for future events.

## Preview locally

```bash
python -m http.server 8000
# then open http://localhost:8000
```

## Publish with GitHub Pages

1. Push this repo to GitHub.
2. **Settings → Pages → Build and deployment → Source: _Deploy from a branch_.**
3. Branch: `main`, folder: `/ (root)`. Save.
4. The site goes live at `https://<user>.github.io/<repo>/` within a minute or two.

## Reuse this as a template for the next event

Everything you need to change lives in two places:

- **`index.html` `<script>` block** — the `PHOTOS` array (image path + caption + credit,
  in page order) and the `COVER` constant. Add or remove entries freely.
- **`index.html` hero + intro copy** — the year, event title, subtitle, location chips,
  and the intro paragraphs are plain HTML near the top of `<body>`.

Then drop your new JPEGs into `images/` and delete the old ones.

### Regenerating images from raw files

The photos here were extracted from Canon **CR3** raw files (full-resolution embedded
previews, orientation-corrected, downsized to ~2000–2600 px long edge, quality 82).
No Adobe products required — the extraction script uses only Python + Pillow.

## Layout

```
index.html          the album page (structure, style, and photo list)
images/             the photographs (web-sized JPEGs)
README.md
```

## Credits

Photographs © the photographer. All rights reserved.
Event: Asheville Beer Choir — *Songs from 1985* (1985 Prom theme).
