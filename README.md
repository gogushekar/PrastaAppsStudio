# Prasta Apps Studio Website

Simple website for Prasta Apps Studio — includes `app-ads.txt` for AdMob verification.

## Deploy to Vercel (3 steps)

1. Go to [vercel.com](https://vercel.com) → Sign up / Log in with GitHub
2. Click **"Add New Project"** → Import this folder or upload via drag & drop
3. Click **Deploy** — done!

AdMob builds the crawl URL from the **hostname** of your Play Store “Developer website”, then always requests **`/app-ads.txt`** on that host ([Google’s rules](https://support.google.com/admob/answer/9363762)).

Examples:

| Developer website in Play Console | Where AdMob looks first |
|-----------------------------------|-------------------------|
| `https://your-app.vercel.app` | `https://your-app.vercel.app/app-ads.txt` |
| `https://user.github.io/MyRepo` | `https://user.github.io/app-ads.txt` (not under `/MyRepo/`) |

So **GitHub Pages project URLs** (`user.github.io/reponame`) usually **fail** unless you also serve the file at `https://user.github.io/app-ads.txt` (e.g. a separate **`username.github.io`** repo with this file) or you use a **custom domain** on this repo’s Pages so the host is your domain.

**Recommended:** Deploy this repo to **Vercel**, set the Play developer website to your **`https://<project>.vercel.app`** URL (no extra path), then confirm `https://<project>.vercel.app/app-ads.txt` shows your publisher line.

This repo keeps `app-ads.txt` at the **repository root** so `/app-ads.txt` is correct on Vercel and on GitHub Pages **custom domains**.

## Files

- `public/index.html` — Main website
- `app-ads.txt` — AdMob / IAB app-ads.txt (repo root; `public/app-ads.txt` is a duplicate for Vercel “public root” deploys)
- `robots.txt` — Allows AdMob / Google crawlers per [Google’s guidance](https://support.google.com/admob/answer/9776740)
- `vercel.json` — Vercel rewrites + `app-ads.txt` headers

## Google Search Console (HTML file verification)

Google requests the file at **`https://<your-URL-prefix>/google00bee3b0d7d65ce9.html`**. The **URL prefix** in Search Console must match where this site is hosted.

- **GitHub Pages (this repo):** use prefix `https://gogushekar.github.io/PrastaAppsStudio` (include the repo path). If you use only `https://gogushekar.github.io`, Google looks at `https://gogushekar.github.io/google00bee3b0d7d65ce9.html`, which this project does **not** serve.
- **Vercel:** use your deployment origin, e.g. `https://your-project.vercel.app`.
- This repo includes **`.nojekyll`** so GitHub Pages does not run Jekyll on these files.

## AdMob Setup

Checklist aligned with [Resolve issues with app-ads.txt](https://support.google.com/admob/answer/9776740):

| Topic | In this repo |
|--------|----------------|
| File not found / wrong host | AdMob requests `https://<<hostname from Play>>/app-ads.txt` ([crawler rules](https://support.google.com/admob/answer/9363762)). GitHub **project** sites (`github.io/reponame`) still use hostname `github.io`, so the first check is often `https://<user>.github.io/app-ads.txt` (404 unless you use a **user** `username.github.io` repo, **Vercel**, or a **custom domain**). |
| Developer website in Play | Must match where you can serve `/app-ads.txt`. **Play Console → Store presence → Store settings → Store listing contact details → Website.** |
| `robots.txt` blocking crawlers | `robots.txt` allows `Google-adstxt`, `Mediapartners-Google`, `Googlebot`, `AdsBot-Google`, and `*` ([Google guidance](https://support.google.com/admob/answer/9776740)). |
| Wrong format / wrong publisher ID | `app-ads.txt` is one line, ASCII, `google.com` + your `pub-…` + `DIRECT` + `f08c47fec0942fa0`. If AdMob still says “details don’t match”, open **AdMob → Apps → app-ads.txt → How to set up** and **paste the current snippet** from there (IDs can change). |
| Crawler “wrong link” | In AdMob’s **app-ads.txt** status, read the **exact crawled URL**. If it’s not where your file returns 200, add a **redirect** on that host to your real `app-ads.txt`, or change the Play **Website** to a host where `/app-ads.txt` is already correct. |

Steps:

1. Deploy with **Vercel** (import repo; **Root Directory** = repo root). Use your production URL (e.g. `https://<project>.vercel.app`).
2. Set the Play **Website** to that **same HTTPS origin** (recommended fix if you were on `github.io/reponame` only).
3. Confirm in a browser: `https://<that-host>/app-ads.txt` → one plain-text line (no HTML shell).
4. AdMob → **Apps** → **app-ads.txt** → **Check for updates**; allow up to **24 hours** after Play listing changes ([Google note](https://support.google.com/admob/answer/9776740)).

`app-ads.txt` exists at the **repo root** (and a copy under **`public/`** for setups that deploy only the `public` folder). Keep both lines identical if you edit the publisher row.
