# tofadachi-couk-redirect

Forwards `tofadachiaianditsolutionsukltd.co.uk` to the main Tofadachi
website at `tofadachiaianditsolutionsukltd.com`, over HTTPS.

The website itself is not here. It lives in the `website` folder of the
`EnrichT16/OluomaApp` repository. This repository holds nothing but the
forwarding page.

## Why this exists

Namecheap can forward a domain on its own, through a URL Redirect
Record, and that was the first arrangement. It only answers on plain
HTTP. It holds no certificate for the domain, so visiting the co.uk over
HTTPS hung until the browser gave up. Since browsers now try HTTPS first
for anything typed into the address bar, that left the co.uk broken for
most visitors.

GitHub Pages issues a real certificate for a custom domain, so publishing
the co.uk as its own small Pages site makes the forward work over HTTPS.
Pages serves one custom domain per site, which is why this cannot live
alongside the .com in the main repository.

## How it works

- `index.html` forwards with `location.replace`, keeping any query string
  and section anchor, so a link to `#products` still lands on the
  products section. `replace` rather than `assign` keeps the co.uk out of
  the visitor's back history, so going Back does not bounce them forward
  again.
- A meta refresh carries anyone with scripting turned off.
- If both fail, the page shows a visible link, in the site palette, with
  a heading and an `en-GB` lang attribute so it reads properly aloud.
- `404.html` is the same page, so every path on the co.uk forwards rather
  than only the root.
- `noindex` and a canonical link point search engines at the .com, so the
  real site is credited rather than this doorway.

## Settings this depends on

- Pages source: deploy from the `main` branch, root folder.
- Custom domain: `tofadachiaianditsolutionsukltd.co.uk`, set by `CNAME`.
- Enforce HTTPS: on, once the certificate has been issued.
- DNS at Namecheap: the four GitHub Pages A records on `@`, and a CNAME
  on `www` pointing at `enricht16.github.io`.
