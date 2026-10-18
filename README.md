# frontdesk-media

Shared, public hosting for the fixed files of websites built inside Frontdesk's Website Builder: logos, decorations, fonts and fallback pictures.

## Why this exists

Frontdesk sites are made of Custom HTML sections, and those sections load fonts and images by URL. Frontdesk's own file storage can't do everything a site needs:

- it refuses font files
- it sends no CORS header, which fonts need inside a section
- it shrinks uploads to 1000px

This repo holds those files instead, and [jsDelivr](https://www.jsdelivr.com/) serves them from GitHub with the right headers and caching.

## Layout

One folder per site, files directly inside it (no deeper folders), so two sites can never clash:

```
dear-vendors/
  logo.svg
  lastik-400.woff2
  yellow-flower.webp
  ...
another-site/
  ...
```

## Using a file

```
https://cdn.jsdelivr.net/gh/dadateniola/frontdesk-media@main/<site>/<file>
```

For example: `https://cdn.jsdelivr.net/gh/dadateniola/frontdesk-media@main/dear-vendors/logo.svg`

Each site's code keeps this address in one setting (for Dear Vendors, `media` in its `config.json`), so the site folder name only appears in one place.

## What belongs here

- **Yes:** files the site always shows and the client never changes: logos, decorative images (flowers, shapes, textures), fonts, background art, placeholders (for example a picture for events that have none).
- **No:** pictures the client sets in Frontdesk's Content tab or Media panel. Those live in Frontdesk.
- **No:** anything private. This repo is public: no keys, tokens, client documents or personal photos.

## Adding a site

1. Make a folder named after the site, in lowercase with hyphens (`my-client`).
2. Add the files with short lowercase names (`logo.svg`, `footer-bg.webp`, `heading-700.woff2`).
3. Prepare them first: WebP for pictures (about 2000px wide at most for full-width ones), optimised SVG for logos, WOFF2 for fonts.
4. Commit and push. The files are live on jsDelivr within a few minutes.

## Changing a file

jsDelivr caches `@main` for up to 7 days. After replacing a file, either:

- clear the cache for it: open `https://purge.jsdelivr.net/gh/dadateniola/frontdesk-media@main/<site>/<file>`, or
- give the new version a new name (`logo-v2.svg`) and point the site at it.

Never rename or delete a file a live site still uses: the site would lose it.

## Fonts

Only add fonts whose licence allows hosting them on the web. Trial or "test" fonts usually don't.
