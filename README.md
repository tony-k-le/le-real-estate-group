# L/E Real Estate Group — Website

Marketing website for **L/E Real Estate Group**, a full-service residential property management firm in Long Beach, CA. Single-page, fully responsive, no build step required.

- **Production:** https://lerealestategroup.com
- **Stack:** Static HTML/CSS/JS · Google Fonts · Unsplash imagery
- **Hosting:** Cloudflare Pages (output directory: `public/`)

---

## Repository structure

```
le-real-estate-group/
├── public/                 # ← everything that gets deployed
│   ├── index.html          # the website (single page)
│   ├── 404.html            # branded not-found page
│   ├── favicon.svg         # L/E emblem favicon
│   ├── robots.txt          # crawler rules
│   ├── sitemap.xml         # search engine sitemap
│   ├── _headers            # Cloudflare security headers
│   └── _redirects          # old Squarespace URLs → new sections
├── .github/workflows/
│   └── deploy.yml          # CI/CD: auto-deploy to Cloudflare on push to main
├── wrangler.toml           # Cloudflare Pages project config
├── package.json            # convenience scripts (dev / preview / deploy)
├── .editorconfig           # consistent formatting
├── .gitignore
├── DEPLOY-GUIDE.md          # full go-live + Squarespace export walkthrough
├── LICENSE
└── README.md
```

Everything served to visitors lives in `public/`. Config, CI, and docs live at the repo root and are never deployed.

---

## Local preview

No build step. Either:

```bash
# simplest — any static server
npm run dev            # serves public/ at http://localhost:3000

# or with Cloudflare's emulator (runs _headers/_redirects too)
npm run preview
```

Or just open `public/index.html` directly in a browser (redirects/headers won't apply that way).

---

## Deploying to Cloudflare Pages

You have two options. **Pick one.**

### Option A — Git integration (recommended, zero-config)

1. Push this repo to GitHub (see below).
2. In the Cloudflare dashboard: **Workers & Pages → Create → Pages → Connect to Git**.
3. Select the repository.
4. Build settings:
   - **Framework preset:** None
   - **Build command:** *(leave empty)*
   - **Build output directory:** `public`
5. **Save and Deploy.** Every push to `main` now auto-deploys. Preview deployments are created for pull requests.

### Option B — GitHub Actions (included)

The workflow at `.github/workflows/deploy.yml` deploys on every push to `main`.

1. In Cloudflare, create the Pages project once (Direct Upload, or first run of Option A).
2. In Cloudflare, create an **API token** with the *"Cloudflare Pages — Edit"* permission, and note your **Account ID**.
3. In GitHub: **Settings → Secrets and variables → Actions** → add:
   - `CLOUDFLARE_API_TOKEN`
   - `CLOUDFLARE_ACCOUNT_ID`
4. Push to `main` — the Action runs `wrangler pages deploy public`.

### Manual deploy from your machine

```bash
npm run deploy          # wrangler pages deploy public --project-name=le-real-estate
```

---

## Pushing to GitHub (first time)

```bash
cd le-real-estate-group
git init
git add .
git commit -m "Initial commit: L/E Real Estate Group website"
git branch -M main
git remote add origin https://github.com/<your-username>/le-real-estate-group.git
git push -u origin main
```

---

## Custom domain

After the first deploy, attach the domain in **Cloudflare Pages → your project → Custom domains** (`lerealestategroup.com` and `www.lerealestategroup.com`). SSL is automatic. For an apex domain, the domain's DNS should be on Cloudflare's nameservers. Full walkthrough (including pointing the domain and exporting the old Squarespace site) is in **`DEPLOY-GUIDE.md`**.

---

## Editing the site

- **Content & layout:** all in `public/index.html` (HTML, CSS, and JS are in that one file).
- **Brand colors / type / spacing:** the CSS custom properties (design tokens) at the top of the `<style>` block — `--ink`, `--bone`, `--accent`, type scale, spacing scale, etc.
- **The logo:** an inline SVG (single vector path) in the nav and footer, recolored via `currentColor`.
- **Redirects:** edit `public/_redirects` if URLs change.
- **Sitemap/robots:** update `public/sitemap.xml` and `public/robots.txt` if you add pages.

### Known follow-ups (not yet wired)

- **Photography** loads from the Unsplash CDN and **fonts** from Google Fonts. To fully self-contain the site, download the images into `public/images/` and repoint the URLs in `index.html`.
- **Forms** (contact, referral, applications) are visual only — they don't submit anywhere yet. Wire them to a form service (Formspree, Basin) or a Cloudflare Pages Function.

---

## Contact

Site contact: `tony@lerealestategroup.com`
