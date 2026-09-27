# Security policy

## Reporting a vulnerability

Please report security issues privately, not in the public issue tracker.

Use GitHub's **[Report a vulnerability](../../security/advisories/new)** button
on the Security tab. If that isn't available to you, open a normal issue saying
only *"I'd like to report a security issue privately"* — with no details — and a
maintainer will arrange a private channel.

Expect an acknowledgement within a few days. Please give us a reasonable window
to ship a fix before disclosing publicly.

## What counts

Pixal is a desktop application with no server, no accounts and no cloud, so the
threat model is narrower than a web app's. The things that matter most:

- **Anything that sends library data off the machine.** Photos, thumbnails,
  face embeddings, GPS coordinates, OCR text, search queries, filenames or
  library statistics reaching any remote host is the most serious class of bug
  Pixal can have. Report it even if you are not sure it is exploitable.
- **The local API being reachable from outside the machine**, or its
  per-launch token leaking to another local process or to a web page.
- **Path traversal** — any request that can read or write a file outside the
  watched folders and Pixal's own data directory.
- **Arbitrary code execution** from opening a malicious image or video, from a
  crafted EXIF payload, or through the Electron renderer.
- **Data loss**: any path that permanently deletes or overwrites an original
  file without going through the trash flow and its confirmation.

## What doesn't

- The API token appearing in a URL query string. Media elements (`<img>`,
  `<video>`) cannot send headers, the server is on loopback only, and the token
  is regenerated every launch. This is deliberate.
- The ability of a user, on their own machine, to read their own database.
  Pixal does not encrypt the library at rest and does not claim to. Full-disk
  encryption is the right tool for that.
- Map tiles revealing the rough area of your photos to the tile server. This is
  documented in **Settings → Privacy**, is a single toggle, and falls back to a
  bundled offline basemap when turned off.
- Vulnerabilities in third-party ML weights you chose to download.

## Supported versions

The latest release. Pixal has no long-term support branches.
