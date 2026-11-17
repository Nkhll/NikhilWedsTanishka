# Nikhil Weds Tanishka &mdash; Wedding Invite Link

A tiny static page that hands guests off to the Meta AI wedding invite.
Free hosting on GitHub Pages, no domain needed.

**Live URL:** https://nkhll.github.io/NikhilWedsTanishka/

## How it works

Meta AI blocks its invite page from being embedded in an iframe
(`X-Frame-Options: SAMEORIGIN` + `frame-ancestors` CSP), so masking the link
behind our own URL is not possible. Instead this page shows a branded card and
jumps to the invite after 150&nbsp;ms, with a button as a fallback for
in-app browsers that block automatic redirects.

## Change the invite URL

Edit **one line** in `config.js`:

```js
window.WEDDING = {
  inviteUrl: "https://www.meta.ai/share/a/YOUR-NEW-ID/"
};
```

Commit. Done &mdash; no build step, no Actions, nothing else to touch.
(GitHub Pages caches for ~10 minutes; test with `?v=2` on the end of the URL.)

The `href` on the button in `index.html` is a fallback for visitors without
JavaScript. It does **not** need updating, but keeping it in sync is harmless.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The page: card, redirect, link previews |
| `config.js` | **The invite URL. The only file to edit.** |
| `preview.jpg` | Optional 1200&times;630 image for WhatsApp link previews |
| `.nojekyll` | Do not delete |
| `README.md` | This file |

`preview.jpg` is not committed yet. Until it exists, the WhatsApp preview shows
title and description without a picture. Add a 1200&times;630 crop of the invite
(or a simple floral card with the names), then re-share the link to refresh the
preview.

## Deploying (already done? these are the steps)

1. Commit and push to `main`.
2. Repo **Settings &rarr; Pages**
   - Source: **Deploy from a branch**
   - Branch: **main** / **/(root)**
   - Leave **Custom domain** empty
3. Wait 1&ndash;2 minutes, tick **Enforce HTTPS** when it appears.
4. Test in Incognito on mobile data, then paste the link into WhatsApp to check
   the preview.

## Things that will break the link

- **Renaming the repository.** The Pages URL changes and every printed QR code dies.
- **Adding a `CNAME` file.** Only add one if you actually own that domain.
- **Deleting the Meta AI chat or the share link.** The redirect then dead-ends.

## QR code

Generate the QR code **after** the site is live and point it at the
`github.io` URL above &mdash; never at the `meta.ai` link.
