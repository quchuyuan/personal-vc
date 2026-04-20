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

## Structure

- `index.html` — the site
- `vercel.json` — clean URL config

`design_files/` (gitignored) holds the original Claude Design source bundle locally.
