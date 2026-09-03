# Sift — public site

Landing page plus the legal documents Meta App Review and App Store Connect
require. Static HTML, no build step, no external dependencies — published with
GitHub Pages.

## Pages

| File | URL path | Purpose |
|---|---|---|
| `index.html` | `/` | Landing page (Turkish) |
| `privacy.html` | `/privacy.html` | Privacy policy (Turkish) |
| `privacy.en.html` | `/privacy.en.html` | Privacy policy (English) — the one to give Meta reviewers |
| `terms.html` | `/terms.html` | Terms of service (Turkish) |
| `terms.en.html` | `/terms.en.html` | Terms of service (English) |
| `support.html` | `/support.html` | Support (Turkish) — the **Support URL** and the **Account deletion URL** in App Store Connect |
| `support.en.html` | `/support.en.html` | Support (English) |

`appstore.png` is the 1024px master icon; `icon-512/180/64.png` are the web-sized
derivatives (regenerate with `sips -Z <size> appstore.png --out icon-<size>.png`).

`style.css` is shared by every page and follows the app's design tokens
(`SiftKit/Sources/SiftDesignSystem/Resources/Colors.xcassets`): amber accent,
warm off-white canvas, automatic light/dark.

## Contact address

`hellosiftapp@gmail.com` is the published contact address, in `privacy.html`,
`privacy.en.html`, `terms.html` and `terms.en.html`. If it ever changes, all
four pages have to change together:

```bash
grep -rl hellosiftapp@gmail.com . | xargs sed -i '' 's/hellosiftapp@gmail.com/new@address/g'
```

## Enabling GitHub Pages

Repository → Settings → Pages → Source: **Deploy from a branch**, branch
`main`, folder `/ (root)`. The site appears at
`https://yasincetindev.github.io/SiftApp/` within a minute or two.

## Keeping it accurate

These documents describe what the app actually does. When behaviour changes —
new data collected, a new processor, a change to the AI or sync model — update
both language versions and the "last updated" date at the top of each page.

Two rules that are easy to get wrong, both learned the hard way:

- **A page may not describe a feature the shipped build does not have.** The
  Instagram DM capture channel ships dark behind `FeatureFlags.instagramDMCapture`
  and is off in release builds, so every section about it was removed for v1.0.
  It goes back in the same commit that flips the flag — the checklist is in the
  app repo at `docs/release/meta-app-review.md` §9.
- **A page may not deny something the app does.** These pages have to agree with
  the App Privacy "nutrition label" in App Store Connect, which Apple reads
  alongside them. Firebase Analytics and the RevenueCat SDK are both in the v1.0
  binary and both are declared on the label, so both are named here.

## Account deletion

Guideline 5.1.1(v) requires an account-deletion route that is reachable from
outside the app. `support.html` carries it, under the `#hesap-silme` /
`#deletion` anchors, and that URL is what goes in the App Store Connect
"Account Deletion URL" field.
