# Life Quality — Indexing Fix Deployment

## Website code fixes included
1. Corrected `robots.txt` sitemap URL.
2. Corrected bad `current-page.html` canonicals in `Newsletter.html` and `lifestyle.html`.
3. Added canonical + robots metadata to `Gallery.html`.
4. Marked `chakrasana-test.html` as `noindex,follow`.
5. Marked fetched standalone component documents (`Components/Navbar.html`, `Components/Footer.html`, `Components/testimonials.html`) as `noindex,follow`.
6. Removed the misleading standalone canonical from the testimonials component.
7. Removed the broken `/yoga.html` component fetch from `js/include.js` because that file does not exist.
8. Rebuilt `sitemap.xml` using canonical public pages only.

## Cloudflare
- Upload **only** `cloudflare-exact-redirects.csv` to a Bulk Redirect List after review.
- Create a separate **Redirect Rule** for `www.lifequality.org.in` → `https://lifequality.org.in` and preserve the path/query. See `CLOUDFLARE-WWW-CANONICAL-RULE.md`.
- Do not upload the old wildcard `www.lifequality.org.in/*` row as a Bulk Redirect list item.

## After deployment
1. Confirm `https://lifequality.org.in/robots.txt` returns the corrected sitemap line.
2. Confirm `https://lifequality.org.in/sitemap.xml` is valid XML and contains only preferred URLs.
3. Test old URLs: each should return one 301 to the intended target.
4. Test target URLs: each should return 200.
5. Confirm no redirect loops/chains.
6. In Google Search Console, inspect representative fixed URLs and start validation for the relevant issue categories.
