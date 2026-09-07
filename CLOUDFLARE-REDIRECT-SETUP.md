# Life Quality — Production Indexing/Redirect Fix

Production hosting: **GitHub → Cloudflare → `lifequality.org.in`**.

## What was fixed in this package
- Removed the obsolete Netlify `_redirects` file.
- Kept the real deployed `.html` pages as the redirect destinations to avoid redirect chains.
- Added a reviewed Cloudflare redirect plan.
- Kept `/retreat` as the real canonical Retreat page.

## Cloudflare — create these in this order
### 1) Bulk Redirect List: Exact legacy redirects
Import `cloudflare-exact-redirects.csv`.

### 2) Bulk Redirect Rule: Exact legacy redirects
Enable the exact list.

### 3) Bulk Redirect List: WWW canonicalization
Import `cloudflare-www-canonical.csv`.

### 4) Bulk Redirect Rule: WWW canonicalization
Enable the WWW list **after** the exact legacy rule. This catches remaining `www.lifequality.org.in/*` requests and sends them to the HTTPS non-www host while preserving the path and query string.

Cloudflare's matching rules allow the more specific path to win within Bulk Redirect matching, and rule order can be used to keep the exact legacy list first.

## Important
Do not import URLs from `academic.lifequality.org.in` or `practice.lifequality.org.in` into this main-site list. They are separate subdomain workstreams.

## Verification
For every redirect: source → **one 301** → final deployed URL returns **200**. Check for loops and confirm query strings are preserved.
