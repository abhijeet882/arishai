# Arish AI — Website

Static one-page site. No build step, no dependencies — just HTML, CSS, and JS in a single file plus an `assets` folder for images and videos.

## Folder structure

```
.
├── index.html          ← the entire site (structure, styles, and scripts)
└── assets/
    ├── carousel-*.jpg  ← "AI in Action" carousel images
    ├── demo-*.mp4       ← product walkthrough videos
    └── poster-*.jpg     ← video poster/thumbnail images
```

**Important:** `index.html` and `assets/` must stay in the same folder, next to each other. If you only download/move `index.html` by itself, images and videos will not appear — this is the most common cause of a "blank" site.

## Before you push: how to preview this properly

**Don't just double-click `index.html`.** Opening a site directly from your file system (a `file://` URL) is unreliable for video playback in most browsers — a browser limitation, not a bug in the site. Images usually still work this way; video often doesn't.

To preview exactly what visitors will see on GitHub Pages, run a tiny local server from this folder:

```bash
npx serve .
```

Then open the URL it prints (e.g. `http://localhost:3000`). Everything — carousel, videos, chatbot, cookie banner — should work there exactly as it will on the live site.

**If images/videos still don't appear**, check that your folder looks exactly like this:
```
your-folder/
├── index.html
└── assets/
    └── ...
```
not
```
your-folder/
└── some-other-folder/
    ├── index.html
    └── assets/
```
Some unzip tools create an extra nested folder — that's the #1 cause of "nothing loads."

## Deploying with GitHub Pages

1. Create a new repository on GitHub (e.g. `arish-ai-website`).
2. Upload everything in this folder to the repository, keeping the same structure — `index.html` at the repo root, `assets/` as a folder next to it.
   - Easiest way: on the repo page, click **Add file → Upload files**, then drag in `index.html` and the `assets` folder together.
   - Or via git:
     ```bash
     git init
     git add .
     git commit -m "Initial site"
     git branch -M main
     git remote add origin https://github.com/<your-username>/<your-repo>.git
     git push -u origin main
     ```
3. In the repository, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Under **Branch**, select `main` and folder `/ (root)`, then click **Save**.
6. GitHub will give you a live URL, typically:
   ```
   https://<your-username>.github.io/<your-repo>/
   ```
   It can take a minute or two to go live after the first save.

## Using a custom domain (optional)

If you want this served at `www.arishai.co.in` instead of the github.io URL:
1. In **Settings → Pages → Custom domain**, enter your domain and save (this creates a `CNAME` file in your repo automatically).
2. At your domain registrar, add a `CNAME` record pointing `www` to `<your-username>.github.io`.
3. Wait for DNS to propagate (can take up to a few hours), then check "Enforce HTTPS" back in the Pages settings once it's available.

## Notes

- The enquiry chatbot sends messages via `mailto:` — it opens the visitor's own email app pre-filled and addressed to `contact@arishai.co.in`. There's no backend, so nothing is sent silently from your server.
- The cookie consent banner stores a preference cookie in the visitor's browser; no analytics are wired up yet, so nothing is actually tracked today even after consent.
- Videos total ~17MB — fine for GitHub Pages, but if you add many more, keep an eye on total repo size (GitHub recommends staying well under 1GB).
