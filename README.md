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
