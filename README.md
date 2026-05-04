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
- `app-ads.txt` — AdMob / IAB app-ads.txt (repository root)
- `robots.txt` — Allows AdMob / Google crawlers per [Google’s guidance](https://support.google.com/admob/answer/9776740)
- `vercel.json` — Vercel rewrites + `app-ads.txt` headers

## AdMob Setup

1. Deploy with **Vercel** (import repo; leave **Root Directory** as the repo root). After deploy, copy your production URL (e.g. `https://prasta-apps-studio.vercel.app`).
2. In **Play Console → Grow users → Store presence → Store settings** → **Store listing contact details**, set **Website** to that same HTTPS origin (path optional for the listing; AdMob still uses **host** + `/app-ads.txt`).
3. In AdMob → **Apps** → **app-ads.txt**, use **Check for updates**. Allow up to 24 hours after changing the Play listing.
4. Test in a browser: `https://<your-exact-host>/app-ads.txt` must show one line: `google.com, pub-6125362256395053, DIRECT, f08c47fec0942fa0` (plain text, no HTML). In AdMob’s status screen, confirm the **crawled URL** matches what you tested.

If the crawled URL is `https://gogushekar.github.io/app-ads.txt` but you only use GitHub **project** Pages, that URL will 404 until you add `app-ads.txt` to a **`gogushekar.github.io`** user site repo, switch the Play website to your **Vercel** host, or attach a **custom domain** to this project’s Pages.
