# vadovado-landing

Static one-page site for **vadovado.com** — the public landing page for
the VadoVado iOS + Mac trip planner.

Pure HTML + inline CSS. No build step, no JavaScript, no dependencies.

> The app itself lives in a separate, **private** repo
> (`stevefabiani/travel-planner`). This repo is intentionally public so
> GitHub Pages can serve it on the free tier.

## Structure

```
.
├── index.html       The one-pager
├── assets/
│   ├── favicon.svg
│   ├── apple-touch-icon.png
│   ├── logo-horizontal.svg
│   └── mark.svg
├── CNAME            "vadovado.com" (GitHub Pages custom-domain marker)
├── .gitignore       .DS_Store / editor scratch
└── README.md
```

Brand assets are copied from the app repo's `vadovado-brand/` design kit.
If the brand evolves, copy the updated SVGs/PNGs from there.

## Local preview

```bash
python3 -m http.server 4173      # or any static server
# open http://localhost:4173
```

## Deploy — GitHub Pages

1. **Push this repo to GitHub** (public). See "First push" below.
2. Repo → **Settings → Pages**:
   - **Source:** Deploy from a branch.
   - **Branch:** `main` / `/ (root)`.
3. **Custom domain:** enter `vadovado.com` → Save.
4. At your domain registrar, point the apex at GitHub Pages:

   ```
   A   @   185.199.108.153
   A   @   185.199.109.153
   A   @   185.199.110.153
   A   @   185.199.111.153
   ```

   Optionally add `CNAME www → stevefabiani.github.io` so `www.vadovado.com`
   also resolves.

5. Wait a few minutes; Pages will provision a Let's Encrypt cert. Enable
   **Enforce HTTPS** in the Pages settings once it's available.

Every push to `main` redeploys automatically. No CI needed.

## First push

```bash
cd ~/Documents/Coding/vadovado-landing
git init -b main
git add .
git commit -m "Initial commit — vadovado.com landing one-pager"
gh repo create vadovado-landing --public --source=. --push --description "Landing site for vadovado.com"
```

(Uses GitHub CLI. Authenticate with `gh auth login` first if needed.)

## Why a separate repo

The VadoVado app repo is private (vault format, key-management details,
historic OAuth artifacts). The landing site is intentionally public so
GitHub Pages can serve it on the free tier and so anyone can read the
copy / file a PR if they spot a typo. Keeping them separated also keeps
the two release cadences independent.

## Privacy policy

The footer links to `/privacy/`. Plan: drop a re-skinned `privacy/index.html`
in this repo when the policy is ready (it's A2 in the app's open-items
list — see the app repo's `docs/CURRENT-STATE.md`). Until then the footer
link 404s; harmless for a soft-launch placeholder.

## Updates form

`mailto:hello@vadovado.com` — zero infra. Upgrade to Cloudflare Forms /
Formspree / Buttondown when there's actual signup volume.
