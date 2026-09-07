# Cloudflare — WWW canonical redirect

Do **not** put `www.lifequality.org.in/*` into a Bulk Redirect CSV. Bulk Redirect list items are exact URL entries; the site-wide host canonicalization should be created as a **Cloudflare Redirect Rule**.

## Rule
- Expression: `http.host eq "www.lifequality.org.in"`
- Action: Dynamic Redirect
- Status: `301`
- Target: `concat("https://lifequality.org.in", http.request.uri.path)`
- Preserve query string: enabled

## Expected behavior
- `http://www.lifequality.org.in/` → `https://lifequality.org.in/`
- `https://www.lifequality.org.in/contact` → `https://lifequality.org.in/contact`
- `https://www.lifequality.org.in/?utm_source=idealist` → `https://lifequality.org.in/?utm_source=idealist`

Create this host-level rule separately from `cloudflare-exact-redirects.csv`.
