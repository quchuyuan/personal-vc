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

Two steps, one minute:

1. **Copy the template.** Duplicate `notes/_template.html` to `notes/<your-slug>.html` and fill in:
   - `<title>`, meta description, canonical URL, OG tags at the top
   - The `.meta`, `<h1>`, subtitle, and `.content` body in `<article>`
2. **Register it in the list.** In `index.html`, find the `<script type="application/json" id="notes-data">` block and add a new entry at the **top** of the array:
   ```json
   {
     "date": "2026-04",
     "title": "Your headline",
     "excerpt": "one-line teaser.",
     "kind": "Essay",
     "slug": "your-slug",
     "status": "published"
   }
   ```
   Use `"status": "draft"` to show the item on the homepage as a muted placeholder before the post goes live.
3. **Ship it.** Commit and push — Vercel redeploys on push.
4. **(Optional) Add to sitemap.** Append a `<url>` entry to `sitemap.xml` pointing at `/notes/<your-slug>`.

`cleanUrls` is on in `vercel.json`, so `/notes/your-slug.html` is served at `/notes/your-slug`.

## Structure

- `index.html` — homepage; notes list is data-driven from inline JSON
- `notes/` — one HTML file per post
  - `_template.html` — copy this to start a new post
- `404.html` — styled 404 page
- `og.svg` — Open Graph share image (1200×630)
- `robots.txt`, `sitemap.xml` — crawler directives
- `vercel.json` — clean URL config

> **Before first deploy:** find-and-replace `https://karlqu.com` throughout `index.html`, `notes/*.html`, `sitemap.xml`, and `robots.txt` with your actual production domain.

`design_files/` (gitignored) holds the original Claude Design source bundle locally.
