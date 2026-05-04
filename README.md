# Prasta Apps Studio Website

Simple website for Prasta Apps Studio — includes `app-ads.txt` for AdMob verification.

## Deploy to Vercel (3 steps)

1. Go to [vercel.com](https://vercel.com) → Sign up / Log in with GitHub
2. Click **"Add New Project"** → Import this folder or upload via drag & drop
3. Click **Deploy** — done!

Your `app-ads.txt` must be reachable at the **root path** of whatever URL you set as the developer website in Play Console, for example:
```
https://your-project.vercel.app/app-ads.txt
```
or, for GitHub Pages project sites:
```
https://<user>.github.io/<repo>/app-ads.txt
```

The file lives at the **repository root** (`app-ads.txt`), not under `public/`, so crawlers get `/app-ads.txt` instead of `/public/app-ads.txt` (which fails AdMob verification).

## Files

- `public/index.html` — Main website
- `app-ads.txt` — AdMob / IAB app-ads.txt (repository root)
- `vercel.json` — Vercel config

## AdMob Setup

1. Deploy the site (Vercel with **project root** = repo root, or GitHub Pages from `main` / root).
2. In **Google Play Console → Grow users → Store settings** (or **Monetization setup**), set **Developer website** to the exact HTTPS URL of this site (same host and path prefix you use in the browser — no typos, and match `www` vs bare domain).
3. AdMob crawls `https://<that-domain>/app-ads.txt`. It must return plain text with the publisher line exactly as in your AdMob instructions (no HTML wrapper, UTF-8, no BOM).

If verification still fails, open your developer URL + `/app-ads.txt` in a private window and confirm you see a single line starting with `google.com, pub-6125362256395053`.
