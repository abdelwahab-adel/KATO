# KATO – كاتو | Website

Static site: HTML5 + CSS3 + vanilla JavaScript (no frameworks, no build step).

```
index.html about.html services.html projects.html contact.html why.html faq.html 404.html
service-electrical|plc|hvac|water|plumbing|contracting.html
style.css   script.js   assets/   _headers   .htaccess   robots.txt
```

## Run
Open `index.html`, or serve the folder (`python3 -m http.server`). Language toggle: AR/EN (button in header).

## Edit content
All text/data lives at the top of `script.js` (object `D`); English strings are in the same file (object `E` + dictionary lines).

## Security
- Strict CSP (meta tag in every page + `_headers`/`.htaccess` for real HTTP headers). Only `fonts.googleapis.com`, `fonts.gstatic.com` and `www.google.com` (map) are allowed.
- No inline scripts, no `eval`, no user input reaches `innerHTML`; form data is length-capped, stripped of control characters and sent only inside a `wa.me` URL (`encodeURIComponent`).
- External links use `rel="noopener noreferrer"`; the map iframe is sandboxed.
- Deploy with HTTPS and enable the HSTS line in `_headers` / `.htaccess`.

## To replace before launch
- Photos in `assets/` (currently low-resolution placeholders), `assets/logo.png` (use the original vector/PNG).
- `robots.txt` sitemap line and an `sitemap.xml` with the real domain.
