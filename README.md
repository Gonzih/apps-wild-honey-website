# Wild Honey on The Porch — Website

Static marketing + App Store compliance site for **Wild Honey on The Porch LLC**.

## Why it exists

App Store review requires a real developer web presence with a reachable
**support URL** and **privacy policy URL**. This site provides both, plus a
showcase for shipped and upcoming apps.

- `index.html` — home: apps, about, open source, contact
- `support.html` — **App Store Support URL** → `/support.html`
- `privacy.html` — **App Store Privacy Policy URL** → `/privacy.html`
- `terms.html` — EULA / Terms of Service
- `styles.css` — single stylesheet, light + dark via `prefers-color-scheme`
- `assets/favicon.svg` — honeycomb + bird mark

## Stack

None. Hand-written HTML/CSS, one small inline script for the copyright year and
scroll reveal. No build step, no dependencies, no external requests — every
graphic is inline SVG.

## Local preview

```sh
python3 -m http.server 8000
# → http://localhost:8000
```

## Deploy

Any static host. Drop the directory at the web root.

**Cloudflare Pages**
```sh
npx wrangler pages deploy . --project-name=wild-honey-website
```

**GitHub Pages** — push to a repo, enable Pages on the default branch, root dir.

**Netlify / Vercel** — no build command, publish directory `.`

## Before going live

- [ ] Point `wildhoneyontheporch.com` (or chosen domain) at the host
- [ ] Update the domain in `sitemap.xml` and `robots.txt` if it differs
- [ ] Swap the support email if a dedicated `support@` address is set up
      (it lives only inside `mailto:` hrefs — see the contact convention below)
- [ ] Fill in the LLC's state of organization in `terms.html` §11 if desired
- [ ] Replace "Coming to the App Store" with the real App Store badge + link
      once Void Tarot is live

## Contact convention

**No personal names anywhere on the site**, and the email address is **never
rendered as visible text** — it exists only inside `mailto:` hrefs behind
"Contact us" buttons and link phrases. This keeps it off scrapers and keeps the
company, not an individual, as the visible party.

Each entry point carries a pre-filled `?subject=` so incoming mail sorts itself
(Void Tarot support, Simorgh, Press, Privacy Request, Terms).

When editing, keep the address out of link text:

```html
<!-- yes -->  <a class="btn primary" href="mailto:…?subject=Support%20request">Contact us</a>
<!-- no  -->  <a href="mailto:…">someone@example.com</a>
```

Verify with:

```sh
grep -rniE "mishelle|weaver|matt" *.html   # should return only mailto: hrefs
```

## Apps

| App | Status | Platform | Source (private) |
|---|---|---|---|
| Void Tarot | Releasing first | iOS 26+, Swift/SwiftUI | `Gonzih/void-tarot` |
| Simorgh | V1 in development | iOS + Android, Expo/RN | `simorgh-app/simorgh-mobile-app` |

Both repos are **private**, so the site deliberately links to neither — a
reviewer clicking through to a 404 is worse than no link. The "How we build"
section replaces what would have been an open-source section. If either repo is
made public later, add the links back to `index.html#craft` and `support.html`.

Site copy is derived from each repo's canonical specs (`docs/mobile-app-spec.md`,
`docs/premium-readings-spec.md`, `PROJECT_SPEC.md`). **If app behavior changes,
the privacy policy and support FAQ must be re-checked against it** — several
claims on this site (on-device generation, CloudKit-only sync, no account,
approximate-location safety help) are load-bearing for App Store review.
