# Elliana

A self-contained single-page web app (KPI / sales dashboard). Everything lives in
one `index.html` file — no build step, no backend, no dependencies. It is responsive
and works on **iPhone, Android, and desktop**, and can be **installed to the home
screen** as an app (PWA: manifest + icons + standalone display).

## Run locally

Just open `index.html` in any modern browser. That's it.

Optionally serve it over HTTP:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy on Netlify

This folder is ready for Netlify as-is (`netlify.toml` and `_redirects` are included,
so deep links fall back to `index.html`). Pick whichever way is easiest.

### Option A — Drag & drop (fastest, no account setup)

1. Go to https://app.netlify.com/drop
2. Drag this whole folder onto the page.
3. Netlify publishes it instantly and gives you a live URL
   (e.g. `https://random-name.netlify.app`). Done.

### Option B — Netlify CLI

```bash
npm install -g netlify-cli
cd elliana-app          # the folder containing index.html
netlify deploy --prod   # follow the prompts; publish directory is "."
```

### Option C — Connect a Git repo (auto-deploy on every push)

1. Push this folder to a GitHub/GitLab/Bitbucket repo.
2. In Netlify: **Add new site → Import an existing project** and select the repo.
3. Build settings: leave **Build command** empty, set **Publish directory** to `.`
   (these are already declared in `netlify.toml`, so you can just accept them).
4. Click **Deploy**. Every push to the repo now redeploys automatically.

## Install as an app (iPhone / Android / desktop)

Once it's live over HTTPS (Netlify gives you HTTPS for free):

- **iPhone (Safari):** Share → **Add to Home Screen**.
- **Android (Chrome):** menu ⋮ → **Install app** / **Add to Home screen**.
- **Desktop (Chrome/Edge):** the install icon in the address bar.

It then launches full-screen like a native app.

## What's in this folder

| File | Purpose |
|------|---------|
| `index.html` | The entire app (HTML + CSS + JS). |
| `manifest.webmanifest` | PWA metadata so the app is installable. |
| `icon-*.png` | App / home-screen icons (192, 512, maskable, iOS 180). |
| `netlify.toml` | Netlify config: no build step, SPA fallback, headers. |
| `_redirects` | SPA fallback (backup to `netlify.toml`). |
| `.nojekyll` | Harmless; only relevant to GitHub Pages. Safe to keep or delete. |

## Notes

- No analytics, no tracking, no external requests — fully offline-capable once loaded.
- Mobile niceties already handled: notch-safe layout (`safe-area-inset`), 44px touch
  targets, a slide-in sidebar drawer on small screens, dark-mode `theme-color`, and
  16px form inputs so iOS doesn't auto-zoom on focus.
