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

All content is **static HTML** (no build step, and it renders even with JavaScript
off — JS only powers the click-to-enlarge lightbox and the twinkle animations). To
adapt it, edit `index.html`:

- **Hero** — the cursive tagline, the big year, the title/subtitle, and the
  `ADMIT ONE` ticket (venue + date) are near the top of `<body>`. Swap the hero photo
  by changing the `background-image` on `.hero__bg`.
- **Dance card (set list)** — each song is one `<li><a class="song" href="…&t=SECONDSs">`
  row inside `<ol class="songs">`; the `t=` value is the deep-link into the concert
  video. Change `VIDEO_URL`-style links and the `watch-cta` button to your recording.
- **Gallery** — each photo is one `<figure class="card">` inside `.masonry`. Add,
  remove, or reorder them; the lightbox picks them up automatically.
- **Footer** — credits (director, video, copyright) live in `<footer>`.
- **Boot intro** — the `#boot` overlay (a 1985 C64-style loading screen with ASCII-art
  letters) shows once per browser session; edit its `.boot__art` `<pre>` to change the
  banner. It's hidden without JavaScript, so it never blocks the content.

Then drop your new JPEGs into `images/` and delete the old ones. The retro palette,
disco ball, balloons, twinkle lights, and film-grain are all pure CSS in the `<style>`
block — recolor via the CSS variables in `:root`.

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

- **Event:** Asheville Beer Choir — *Songs from 1985* (1985 Prom theme), The Funkatorium, Asheville NC, Aug 29 2026
- **Founder & Choir Director:** Laura Williams — [ashevillebeerchoir.com](https://www.ashevillebeerchoir.com/team)
- **Concert video:** Brandon
- **Photographs:** © 2026, all rights reserved

The set list links deep-link into the concert recording on the Asheville Beer Choir
YouTube channel.
