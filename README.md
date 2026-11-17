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
| `preview.jpg` | 1200&times;630 screenshot used for WhatsApp link previews |
| `qr.svg` | Vector QR code &mdash; use this for printing |
| `qr.png` | 1200&times;1200 QR code &mdash; WhatsApp stories / screens |
| `.nojekyll` | Do not delete |
| `README.md` | This file |

The page deliberately mirrors the invite's opening screen &mdash; cream
`#FCF8EF`, navy `#152A47`, gold `#C7A76A`, "Jai Shree Mataji", date and venue
&mdash; so the hand-off to `meta.ai` feels seamless. Keep that in mind if you
change the artwork; update the hex values and the `.when` line in `index.html`
along with `preview.jpg`.

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

`qr.svg` and `qr.png` both encode `https://nkhll.github.io/NikhilWedsTanishka/`
(never the `meta.ai` link), navy `#152A47` on cream `#FCF8EF`, error correction
level **H**, with a 3-module quiet zone. Both were verified by decoding them
back to the URL.

- **`qr.svg`** &mdash; true vector, 37&times;37 modules. Use this for the printed
  invitation. Print at **at least 25&times;25 mm**; if the card is glossy, keep
  the cream background or place it on white.
- **`qr.png`** &mdash; 1200&times;1200 for stories and screenshots.

Never crop the cream margin &mdash; scanners need that quiet zone. If the URL
ever changes, regenerate:

```powershell
$u = "https://nkhll.github.io/NikhilWedsTanishka/"
$enc = [uri]::EscapeDataString($u)
$base = "https://quickchart.io/qr?text=$enc&ecLevel=H&margin=3"
curl.exe -s "$base&format=svg&size=1000&dark=152A47&light=FCF8EF" -o qr.svg
curl.exe -s "$base&format=png&size=1200&dark=152A47&light=FCF8EF" -o qr.png
```
