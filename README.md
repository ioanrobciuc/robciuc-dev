# robciuc-dev

Personal site for [robciuc.dev](https://robciuc.dev) — Ioan Robciuc, Software Developer.

Plain static HTML + CSS, hosted on GitHub Pages. No build step, no framework, no dependencies.

## Run locally

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

## Structure

```
index.html            the page: header, hero, Experience, Apps, footer
css/style.css         all styles; design tokens are CSS variables in :root
favicon.svg           browser icons
favicon-32.png
apple-touch-icon.png
assets/
  videowise-icon.png  app icon (Apps section)
  sigla/              logo files (wordmark + symbol, light/dark, SVG + PNG)
robots.txt            search engines
sitemap.xml
CNAME                 custom domain for GitHub Pages (robciuc.dev)
.nojekyll             tells GitHub Pages to serve files as-is
```

All paths in `index.html` are relative, so the site works on the custom domain and on
`<user>.github.io/robciuc-dev/` alike.

## Design tokens

Defined once in `css/style.css` (`:root`):

| Token | Value |
| --- | --- |
| Background | `#0C0C0E` |
| Text | `#f8fafc` |
| Text soft / muted / dim | `#cbd5e1` / `#94a3b8` / `#64748b` |
| Border | `#1e293b` |
| Accent | `#C0F447` |
| Logo ink | `#F7F7F4` |
| Fonts | Inter (body), Geist (wordmark), from Google Fonts |
| Radius | 6px buttons · 8px cards · 999px pills |
| Max width | 720px |

## Editing content

Everything lives in `index.html`.

- **Add a job:** copy a `<li class="job">` block inside `<ul class="card jobs">`. Newest goes first.
  Add `<span class="pill pill--current">Current</span>` for an ongoing role; wrap the company name in a link
  (with the `#i-arrow-up-right` icon) if it has a website.
- **Add an app:** copy the `<article class="card app">` block in the Apps section.
- **Social links:** they appear twice, in the hero and in the footer; update both.
- **Icons:** Tabler-style SVGs (stroke 2, 24 viewBox) defined once in the sprite at the top of `<body>`
  and used with `<svg><use href="#i-name"/></svg>`. To add one, add a `<symbol id="i-name">`.
- **Footer year:** `Copyright © 2023 - 2026` is hardcoded; update it each year.

When adding pages, also list them in `sitemap.xml`.

## Deploy (GitHub Pages)

1. Push to GitHub.
2. Repo → Settings → Pages → Source: **Deploy from a branch**, branch `development`, folder `/ (root)`.
3. `CNAME` sets the custom domain to `robciuc.dev`. At the DNS provider, point the apex domain to GitHub Pages
   with A records `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   (optionally a `www` CNAME to `<user>.github.io`).
4. Tick **Enforce HTTPS** once GitHub issues the certificate — `.dev` domains only work over HTTPS.

Every push to `development` redeploys the site.
