# Prasta Apps Studio Website

Simple website for Prasta Apps Studio — includes `app-ads.txt` for AdMob verification.

## Deploy to Vercel (3 steps)

1. Go to [vercel.com](https://vercel.com) → Sign up / Log in with GitHub
2. Click **"Add New Project"** → Import this folder or upload via drag & drop
3. Click **Deploy** — done!

Your `app-ads.txt` will be live at:
```
https://your-project.vercel.app/app-ads.txt
```

## Files

- `public/index.html` — Main website
- `public/app-ads.txt` — AdMob ads.txt file
- `vercel.json` — Vercel config

## AdMob Setup

After deploying, go to:
**Google Play Console → Monetize → app-ads.txt**
and enter your Vercel domain as your developer website URL.
