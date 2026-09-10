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
balloons, twinkle lights, and film-grain are all pure CSS in the `<style>`
block — recolor via the CSS variables in `:root`.

### Regenerating images from raw files

The photos here were extracted from Canon **CR3** raw files (full-resolution embedded
previews, orientation-corrected, downsized to ~2000–2600 px long edge, quality 82).
No Adobe products required — the extraction script uses only Python + Pillow.

## Lessons learned (read before building the next one)

Hard-won notes from building this album, so the next goes faster.

### Getting photos out of the raws
- **Canon CR3 (and most raw formats) embed a full-resolution JPEG preview** you can
  pull out with just Python + Pillow — no Adobe, no raw developer. Scan the file for
  JPEG markers (`FF D8 … FF D9`) and keep the largest one.
- **Orientation is the trap.** That embedded preview has *no* rotation tag — the
  orientation lives in the CR3's own metadata (the `CMT1`/EXIF box). If you don't read
  it and rotate, every portrait comes out sideways. (Phone JPEGs *do* carry EXIF
  orientation — use Pillow's `ImageOps.exif_transpose`.)
- **Export size:** ~2000 px on the long edge, JPEG quality ~82, progressive. Crisp on
  screen, small files — the whole 45-photo album is well under 15 MB.
- **Phone files** may be named `….MP.jpg` (Motion Photo) or `….PORTRAIT.jpg`; they open
  fine as ordinary JPEGs.

### Choosing the photos
- Extract a **sample across the whole shoot** (every Nth frame), build **contact-sheet
  montages**, and review those to pick finalists — far faster than opening hundreds of
  files. Then export just the finalists at full web size.
- Watch for **near-duplicate bursts** and keep only the best of each. If the photos live
  in a tool that clusters similar frames, that grouping does the culling for you.

### Design traps that cost real time
- **Single-weight display fonts get fake-bolded and ruined.** A decorative font like
  *Monoton* ships in only one weight, but headings (`<h1>/<h2>`) are **bold by default**,
  so the browser *synthesises* bold by thickening the strokes — which closes up the
  font's fine detail, and does it **differently on each computer** (looked fine on one
  screen, bad on another). Always set **`font-weight:normal` and `font-synthesis:none`**
  on such fonts.
- **Thin-line lettering needs contrast.** Over a busy photo, the gaps in a pinstripe
  font wash out; put a **soft dark backing** behind the lettering so the detail reads on
  any screen.
- **Don't blur detailed lettering.** A large `text-shadow` glow bleeds into the thin
  gaps and fills them — use a **hard, zero-blur offset shadow** instead.
- **Test on a second computer/browser.** Font rendering and screen sharpness vary; a
  high-DPI monitor hides problems a normal one reveals.

### Keep the content static
- **Put the real content (images, captions, text) in plain HTML, not injected by
  JavaScript.** It then renders everywhere — with JS disabled, in link previews, in
  editor snapshots. Use JS only for *extras* (the lightbox, the animations).
- If you use the HTML `hidden` attribute, include a **`[hidden]{display:none!important}`**
  reset — a `display:` rule on the element otherwise overrides `hidden` and it never
  hides (this once let an overlay cover the whole page).

### Hosting on GitHub Pages
- **Structure:** `index.html` at the repo root, an `images/` folder, this README.
  Turn it on at **Settings → Pages → Deploy from a branch → `main` / `(root)`**; it goes
  live at `https://<user>.github.io/<repo>/`.
- **The social-preview image needs an ABSOLUTE URL.** `og:image` as a relative path
  (`images/card.jpg`) will **not** show in Discord/Slack/iMessage — they can't resolve
  it. Use the full `https://<user>.github.io/<repo>/images/og-card.jpg`, and add
  `og:image:width`/`height`/`type`, `og:url`, `twitter:card=summary_large_image`, and a
  `theme-color`. Make a dedicated **1200×630** card image.
- **Caching bites twice.** Pages takes ~1–2 minutes to rebuild and clear its CDN after a
  push — verify with a cache-busting query (`?v=2`). Browsers cache the CSS and chat apps
  cache the link preview, so after a change **hard-refresh** (Shift+reload), and expect an
  already-shared link to keep its old preview for a while.
- **It's public and indexable.** Photos of identifiable people go on an open URL — fine
  when intended, worth a conscious choice. No private data in the repo.

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
