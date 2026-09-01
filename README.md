# The'Salat — website

Marketing site + legal pages (Privacy Policy, Support) for the The'Salat iOS app,
required for App Store submission.

- `index.html` — landing page (features, screenshots, mission)
- `demo.html` — the screen capture, on its own page
- `privacy-policy.html` — canonical Privacy Policy URL for App Store Connect
- `support.html` — canonical Support URL for App Store Connect
- Static, no build step. Auto light/dark.

## Where this is served

**https://thesalat.app** — the site's own domain since 2026-09-01, behind Cloudflare.

GitHub Pages is **off**. The old address, `kmohammedsu.github.io/salat-website/*`,
now returns 404 and nothing redirects it, so any URL written down before the move
is dead. Three of them mattered and are fixed in the app repo:
`SalatConfig.privacyPolicyURL`, and the Support and Privacy Policy URLs recorded
in `AppStore/listing.md`. The two in **App Store Connect must still be changed by
hand** — see the note in that file.

`.nojekyll` is a leftover of the Pages era. It is inert now, and harmless.
There is deliberately no `CNAME` file: that is a GitHub Pages mechanism and does
nothing on the current host.

## The App Store link

`download/index.html` is the only page on the site that holds an App Store URL,
and **https://thesalat.app/download** is the short link to hand out. Everything
else, including the badge in the hero, points at that page rather than at the
store, so there is one line to change and no chance of a second copy going
stale:

```html
<a class="btn" id="go" href="https://apps.apple.com/app/id0000000000">
```

Swap the zeros for the real app id. While the id is still all zeros the page
knows the link is not ready: it stays put, greys out the button, and says the
link is being set up, rather than throwing anyone at a broken App Store page.
The moment a real id is in place it redirects on its own, using
`location.replace` so the back button skips the redirect page instead of
trapping people on it.

## Assets

Everything in `assets/` is captured from the shipping build on an iPhone 17 Pro
simulator with the status bar pinned to 9:41, then written out as 720px-wide
WebP. To recapture, take a full-resolution PNG (`xcrun simctl io <udid>
screenshot`) and convert with `cwebp -q 82 -resize 720 0`.

- `home.webp` `nearby-default.webp` `expanded.webp` `widget.webp`
  `cardback.webp` `notif-detail.webp` — the feature tour
- `nearby-rose.webp` `nearby-navy.webp` `nearby-emerald.webp` — the themes strip
- `icon.png` — the app icon, 256px, from `Salat/Salat/Assets.xcassets/AppIcon.appiconset`
  in the app repo
- `og.png` — the 1200×630 social card. `home.png` is a copy of it, kept only so
  links shared before the redesign still resolve to a current image.
- `demo.mp4` + `demo-poster.webp` — the screen capture used on `demo.html`.
  The poster is frame one of the video, so there is no jump when it starts.

App repo: https://github.com/kmohammedsu/salat-app
