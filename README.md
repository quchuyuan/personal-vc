# Karl Qu — Personal Site

Personal website / VC scout landing page. Static HTML, no build step.

## Local preview

Open `index.html` directly in a browser, or run any static server:

```bash
python -m http.server 8000
# then open http://localhost:8000
```

## Deploy to Vercel

1. Push this repo to GitHub.
2. On [vercel.com](https://vercel.com), click **Add New → Project**, import the GitHub repo.
3. Framework preset: **Other** (no build, no output directory).
4. Click **Deploy**. Vercel serves `index.html` from the repo root.

Alternatively, with the Vercel CLI:

```bash
npm i -g vercel
vercel
```

## Publishing a new note

The notes list on the homepage is plain static HTML — no build step, no JSON registry. Paste a link into the list and ship.

1. **Copy the template.** Duplicate `notes/_template.html` to `notes/<your-slug>.html` and fill in:
   - `<title>`, meta description, canonical URL, OG tags at the top
   - The `.meta`, `<h1>`, subtitle, and `.content` body in `<article>`
2. **Add a row to the notes list in `index.html`.** Find `<div class="notes reveal-stagger" id="notesList">` and paste a new entry at the **top**:
   ```html
   <a class="note" href="/notes/your-slug">
     <span class="date">2026 · 04</span>
     <span class="title">Your headline — <span>one-line teaser.</span></span>
     <span class="kind">Essay</span>
   </a>
   ```
   The kind is free text shown as a badge — `Essay`, `Review`, `Guide`, `Thesis`, or `Note`.
3. **(Optional) Add a "currently writing" entry.** The `<p class="notes-upcoming">` line below the list is a free-text list of in-progress titles. Edit it directly.
4. **Ship it.** Commit and push — Vercel redeploys on push.
5. **(Optional) Add to sitemap.** Append a `<url>` entry to `sitemap.xml` pointing at `/notes/<your-slug>`.

The list sort order is manual (newest first) since the list is short. If it grows past a screenful, consider building it from a data file.

`cleanUrls` is on in `vercel.json`, so `/notes/your-slug.html` is served at `/notes/your-slug`.

Production domain: **https://karlqu.space**

## Structure

- `index.html` — homepage; notes list is static HTML
- `notes/` — one HTML file per post
  - `_template.html` — copy this to start a new post
- `404.html` — styled 404 page
- `og.svg` — Open Graph share image (1200×630)
- `robots.txt`, `sitemap.xml` — crawler directives
- `vercel.json` — clean URL config
- `DESIGN.md` — design system reference; read before making UI changes

`design_files/` (gitignored) holds the original Claude Design source bundle locally.
