# Audit report – kato-final

Tools: html5lib (HTML parse), axe-core 4 (WCAG 2.0/2.1/2.2 A+AA + best-practice), ESLint, Stylelint, Playwright/Chromium.
Matrix tested: 14 pages × AR/EN × 320/375/768/1024/1440/1920 px, with the CSP active.

## Fixed
| Area | Finding | Fix |
|---|---|---|
| Bug | `<title>` was forced to the home-page title on **every** page when switching language | Title is now derived per page (AR ⇄ EN) |
| Bug | KPI table overflowed the screen at 320 px (EN) | Wrapped in a scroll container |
| Bug | Accordions allowed several open items | One open at a time (works for dynamically-built accordions) |
| Security | No CSP | Strict CSP meta on all pages + real headers (`_headers`, `.htaccess`) incl. `frame-ancestors`, `nosniff`, Referrer/Permissions-Policy |
| Security | `window.open` without `noopener` | `noopener,noreferrer` |
| Security | Form values unbounded / control chars | `maxlength`, 120/800 char caps, control chars stripped, URL-encoded |
| Security | Map iframe unrestricted | `sandbox` + `referrerpolicy` |
| HTML | Unescaped `&` in URLs; empty `<img src>`-style leftovers | Escaped; 0 parse errors on all 14 pages |
| A11y | 148 contrast failures (#77797d, yellow active link, green, white on yellow) | Colours darkened just enough (≥ 4.5:1); active link keeps yellow underline |
| A11y | Heading order, missing landmarks, clickable cards/gallery not keyboard-reachable, modal focus | h-levels fixed, floating buttons in `<aside>`, real links + keyboard support, dialog semantics + focus return, `aria-invalid` on form errors |
| A11y/i18n | `alt` / `aria-label` / `title` stayed Arabic in EN mode | Translated with the page |
| Perf | `logo.png` 406 KB | 29 KB (same look) · favicon 10 KB · fonts preconnect |
| Code | Unused var, assignment-in-condition, 6 CSS lint errors | ESLint and Stylelint clean |
| Added | `?service=` prefill on the contact form, 404 page, robots.txt, README | – |

## Result
axe: 0 violations (AR/EN, desktop/mobile) · ESLint 0 · Stylelint 0 · HTML parse errors 0 · console errors 0 · overflow 0.

## Not possible to verify here / to do before launch
- Firefox and Safari were not available in the test environment (Chromium only).
- Google Fonts and the map load from Google – self-host the fonts if you want zero third-party requests.
- Replace placeholder photos and the 200×200 logo with originals; add real domain to `robots.txt`/sitemap, canonical and `og:image` (absolute URL).
- A static site has no server-side validation: the form only opens WhatsApp. Add a backend (with rate-limit/CAPTCHA) if you want to store requests.
