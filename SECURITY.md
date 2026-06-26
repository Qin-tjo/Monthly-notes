# Security

Meridian is a single static HTML file. It has no server, no accounts, no
network calls that send your data anywhere, and no analytics. The threat
surface is intentionally small. This document spells out what we do and
do not protect against, and how to report something we missed.

## Threat model

What we protect against:

- **Self-XSS via crafted import file.** All user-controllable data
  (entry text, season title, hue) is HTML-escaped before being placed
  in `innerHTML`. Hue values from imports are coerced to the curated
  list of 24 named pigments. Style attributes that interpolate a colour
  string are guarded by an `escapeAttr` helper that only allows the
  `#xxxxxx` hex shape or short alphanumeric tokens; anything else falls
  back to a neutral grey.
- **Schema-level malice in stored or imported data.** Both the
  `localStorage` loader and the import handler run every field through
  a schema validator (regex on month keys, length caps on prose,
  integer ranges on plate numbers and reminder day, allow-list lookup
  on hues). Unknown fields are dropped.
- **Oversized import files.** Imports above 5 MB are rejected.
- **Supply-chain tampering of the lazy-loaded library.** The PNG
  exporter pulls `html-to-image@1.11.13` from jsDelivr only when the
  user clicks *Download · PNG*. The script tag is loaded with a
  pinned version and an SRI `integrity` hash; any mismatch aborts the
  load and the user can fall back to the PDF exporter, which uses only
  the browser's native print pipeline.
- **Content injection via the page.** A strict Content-Security-Policy
  meta tag restricts script, style, font, image, frame and form
  sources. `frame-ancestors 'none'` prevents clickjacking by embedding;
  `referrer` is set to `no-referrer`.

What we do **not** protect against (and never will, by design):

- **A malicious browser extension** with permission to read the page.
  Any extension you install can read or alter `localStorage`. If your
  notes are sensitive, write them in a browser profile with no
  third-party extensions.
- **A malicious origin you self-host the file from.** If you publish
  Meridian on a domain you also use for other things, code on that
  origin can read your archive. Host it somewhere dedicated, or open
  the `index.html` file directly.
- **Physical access to the device.** Anyone who can unlock your
  browser can read the archive. The app does not encrypt at rest.
- **An adversary on the same machine with access to the browser
  profile directory.** Same as above.
- **Loss of data.** `localStorage` is not a backup. If the browser
  clears site data, the archive is gone. The app surfaces a quiet
  *export to JSON* nudge every three sealed plates for this reason.

## Third-party resources

| Resource | Origin | When loaded | Verification |
| --- | --- | --- | --- |
| Fraunces, Inter (CSS) | `fonts.googleapis.com` | Page load | CSP `style-src` |
| Fraunces, Inter (font files) | `fonts.gstatic.com` | Page load | CSP `font-src` |
| `html-to-image@1.11.13` | `cdn.jsdelivr.net` | First *Download · PNG* click | SRI `sha384-…`, CSP `script-src` |

No telemetry. No analytics. No connection to any other origin.

## Reporting

If you find something we should fix, please open a private issue or
email the maintainer. Please do not file a public issue for anything
sensitive until we have had a chance to respond.
