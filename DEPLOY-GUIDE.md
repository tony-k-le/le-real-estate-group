# L/E Real Estate Group — Go-Live Guide

This guide covers two things:

1. **Exporting/archiving the old Squarespace site** (so you keep your content and can cancel Squarespace later).
2. **Publishing the new design on Cloudflare** and pointing `lerealestategroup.com` at it.

The deployment package is `le-real-estate-cloudflare.zip` (and the unzipped `le-deploy/` folder). It contains everything Cloudflare needs.

---

## What's in the package

| File | Purpose |
|------|---------|
| `index.html` | The new website (your homepage). |
| `404.html` | Branded "page not found" page. |
| `_redirects` | Forwards old Squarespace URLs (`/properties`, `/management`, `/contact-us`, etc.) to the matching sections on the new one-page site, so old links and search results keep working. |
| `_headers` | Basic security headers. |
| `robots.txt` | Lets search engines crawl the site, points to the sitemap. |
| `sitemap.xml` | Tells Google the site exists. |

---

## Part A — Export the old Squarespace site (archive your content)

> Squarespace's export is a content archive (WordPress `.xml`), **not** a working website. You are not reusing it — your new site is already built. This step just preserves your old text/images before you eventually cancel Squarespace.

1. Log in at **squarespace.com** and open the site.
2. Go to **Settings → Advanced → Import / Export** (older accounts: **Settings → Import & Export Content**).
3. Click **Export**, then choose **WordPress** when prompted. Wait for the progress bar.
4. Click **Download** and save the `.xml` file somewhere safe.
5. **Save your images separately.** The XML references images but doesn't bundle them cleanly. Right-click and save any photos you want to keep, or download them from **Settings → Files / Asset Library** if available.

**Heads-up:** Squarespace only exports basic pages and one blog. Galleries, forms, product/event blocks, and any custom styling do **not** export. Keep your Squarespace site **published** until the new site is fully live (Part D), because you can't export from an unpublished/expired site.

---

## Part B — Deploy the new site to Cloudflare Pages

1. Create/log in to a **Cloudflare account** at **dash.cloudflare.com** (free plan is fine).
2. In the left sidebar, go to **Workers & Pages → Create → Pages → Upload assets** (also called **Direct Upload**).
3. Name the project, e.g. `le-real-estate`. Click **Create project**.
4. **Drag and drop the `le-deploy` folder** (or upload the unzipped contents — not the `.zip` itself) into the upload area. Make sure `index.html` sits at the **top level**, not inside a subfolder.
5. Click **Deploy site**. In a few seconds you'll get a live preview at `https://le-real-estate.pages.dev`. Open it and confirm everything looks right.

> To update the site later, repeat steps 2–5 (Create a new deployment / upload assets) with the edited files.

---

## Part C — Point lerealestategroup.com at the new site

How you do this depends on where the domain lives. The cleanest path is to manage DNS in Cloudflare.

### Option 1 — Move the domain's DNS to Cloudflare (recommended for an apex domain)

1. In Cloudflare: **Add a site** → enter `lerealestategroup.com` → choose the Free plan. Cloudflare scans your existing DNS records.
2. Cloudflare gives you **two nameservers** (e.g. `xxx.ns.cloudflare.com`).
3. Log in to wherever the domain is **registered** (likely Squarespace Domains / Google Domains / GoDaddy) and **replace the nameservers** with Cloudflare's two. This can take a few minutes to ~24 hours to propagate.
4. Back in Cloudflare: **Workers & Pages → your Pages project → Custom domains → Set up a domain** → enter `lerealestategroup.com` and again as `www.lerealestategroup.com`. Cloudflare adds the records and provisions SSL (HTTPS) automatically.

### Option 2 — Keep DNS where it is (custom domain via CNAME)

1. In your current DNS provider, add a **CNAME** record:
   - `www` → `le-real-estate.pages.dev`
2. For the bare/apex domain (`lerealestategroup.com` with no `www`), most registrars need a CNAME-flattening/ALIAS record, or you redirect apex → `www`. Apex on Cloudflare Pages works most reliably when the domain is on Cloudflare's nameservers (Option 1), which is why Option 1 is recommended.
3. In Cloudflare Pages → **Custom domains**, add the domain so SSL is issued.

---

## Part D — Cut over and verify

1. Visit `https://lerealestategroup.com` and `https://www.lerealestategroup.com` — both should load the new site over HTTPS (padlock).
2. Test the old links: `lerealestategroup.com/properties`, `/management`, `/contact-us` should redirect to the matching section.
3. Check on a phone.
4. In **Google Search Console**, submit `https://lerealestategroup.com/sitemap.xml`.
5. Once you're happy it's stable for a few days, you can **downgrade/cancel Squarespace**. (Keep your exported `.xml` and images first.)

---

## Recommended before launch (optional but worth it)

- **Self-host the photos.** The site currently loads images from Unsplash's CDN and fonts from Google. They'll work, but if an Unsplash URL ever changes, that image breaks. For full control, download each photo, drop them in an `images/` folder in `le-deploy`, and update the URLs in `index.html` to `images/your-file.jpg`. I can do this for you on request.
- **Email forms.** The contact, referral, and application forms are visual only right now (they don't send anywhere). To make them work on Cloudflare, wire them to a free form endpoint (e.g. Formspree, or a Cloudflare Worker/Pages Function). I can set this up.
- **Add a favicon** and Open Graph preview image for nicer link sharing.

---

## Quick reference

- New homepage file: `index.html`
- Live preview URL (after Part B): `https://<project>.pages.dev`
- Production URL (after Part C): `https://lerealestategroup.com`
- Contact email used on the site: `tony@lerealestategroup.com`
