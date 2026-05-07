# Skimr Landing Page — Vercel Deployment

A static landing page for Skimr, the free Chrome extension that turns any article or PDF into AI-generated Cliff Notes, flashcards, and a recall quiz.

## Files in this folder

| File | Purpose |
|---|---|
| `index.html` | The landing page itself |
| `og-image.png` | Open Graph / Twitter Card preview image (1200×630) |
| `robots.txt` | Search engine crawler instructions |
| `sitemap.xml` | URL sitemap for search engines |
| `README.md` | This file |

---

## Deploy to Vercel (5 minutes, free)

### Option A — Drag and drop (easiest)

1. Sign up at [vercel.com](https://vercel.com) — free for personal projects
2. From the dashboard, click **"Add New..." → "Project"**
3. Scroll to **"Deploy without Git"** or use the upload area, drag this entire folder onto the page
4. Vercel auto-detects it as a static site. Click **"Deploy"**
5. In ~30 seconds, you'll have a URL like `skimr-xyz.vercel.app`

### Option B — GitHub-connected (better for ongoing updates)

1. Create a new GitHub repo (private or public) called `skimr-site`
2. Drag this folder's contents into the repo
3. In Vercel: **"Add New..." → "Project" → import the GitHub repo**
4. Vercel auto-deploys. Future pushes to `main` auto-redeploy.

---

## Connect your custom domain (skimr.app)

The HTML is pre-configured for `https://skimr.app/`. After Vercel deploys:

1. Buy `skimr.app` at [Porkbun](https://porkbun.com) (~$12/yr, no upsells) or [Cloudflare Registrar](https://www.cloudflare.com/products/registrar/) (wholesale pricing)
2. In your Vercel project: **Settings → Domains → Add**
3. Enter `skimr.app`
4. Vercel shows you the exact DNS records to add at your domain registrar (usually a CNAME or two A records)
5. Copy those into your registrar's DNS panel
6. Wait 5–30 minutes for DNS propagation
7. Vercel auto-provisions SSL/HTTPS — no action needed

---

## ⚠️ If you buy a different domain (not skimr.app)

The HTML is pre-configured for `skimr.app`. If you buy something else (e.g., `getskimr.com`), search-and-replace the following before deploying:

In `index.html`:
- 8 occurrences of `https://skimr.app` → your domain

In `robots.txt`:
- One occurrence of `https://skimr.app/sitemap.xml` → your domain

In `sitemap.xml`:
- One occurrence of `<loc>https://skimr.app/</loc>` → your domain

Any modern editor (VS Code, Sublime, Cursor) handles this in 30 seconds with find-and-replace.

---

## Verify SEO is working after deploy

Three free validators — run all three after deploying:

| Tool | What it checks |
|---|---|
| [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/) | Open Graph image, title, description |
| [Twitter Card Validator](https://cards-dev.twitter.com/validator) | Twitter / X social preview |
| [Google Rich Results Test](https://search.google.com/test/rich-results) | SoftwareApplication and FAQPage schemas |

All three should show your OG image rendering and the schemas validating cleanly. If anything fails, the validator tells you exactly what to fix.

---

## Submit to search engines

Once your site is live at your real domain:

1. **Google Search Console** — [search.google.com/search-console](https://search.google.com/search-console)
   - Add property → enter your domain
   - Verify ownership (DNS TXT record or HTML file upload)
   - Submit `sitemap.xml`
2. **Bing Webmaster Tools** — [bing.com/webmasters](https://www.bing.com/webmasters)
   - Same process, also submit sitemap

Within 24–72 hours, search engines will crawl your site and start indexing it.

---

## Updating the page later

The HTML is hand-written and easy to edit. Common updates:

- **New tagline?** Search for "Read once" — appears in `<title>`, `<h1>`, OG/Twitter meta, JSON-LD
- **New feature?** Add another `.feature` div in the `<section class="features">` block. Also update `featureList` in the SoftwareApplication JSON-LD
- **New FAQ question?** Add another `.faq-item` in the `<section class="faq">` block. Mirror it in the FAQPage JSON-LD

After editing, redeploy:
- **Vercel drag-drop:** drag the new `index.html` into the same project (Vercel detects it's a re-upload and replaces)
- **Vercel + GitHub:** commit and push, auto-deploys

---

## What's NOT in this bundle (future improvements)

- **Favicon** — currently the browser shows a default globe. Add a `favicon.png` (32×32 or 64×64) when you have a final visual identity, then add `<link rel="icon" type="image/png" href="/favicon.png">` to `<head>`.
- **Privacy policy / Terms** — not legally required given the no-account / local-storage model, but adds polish. Could be a `/privacy.html` page if you want it.
- **Analytics** — no tracking installed (intentional, fits Skimr's privacy-first stance). If you want install-funnel data later, consider [Plausible](https://plausible.io) or [Fathom](https://usefathom.com) — both privacy-respecting and easy to add.
- **Demo video** — currently hosted on hyperagent.com. To self-host on your own domain, drop the .mp4 file into this folder and update the `<source src="...">` tag in `index.html`.

---

## Questions

If anything breaks during deployment, the most common fixes:

- **Vercel says "no index file"** → make sure `index.html` is at the root of the folder, not nested
- **OG image doesn't show in social shares** → run the Facebook Sharing Debugger and click "Scrape Again" to refresh their cache
- **Custom domain says "DNS error"** → wait another 15 minutes for propagation, or double-check the registrar DNS records match what Vercel showed you

---

Built by Anu Tewari for Skimr.
