# goatyler.com 🐐

The hub for everything Tyler builds. One static page, zero dependencies, zero build step.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole site — HTML, CSS and JS in one file |
| `404.html` | "This goat wandered off" page for bad URLs |
| `CNAME` | Only needed for GitHub Pages custom-domain setup (harmless elsewhere) |

## Adding / editing your sites

Open `index.html` and find the `SITES` array near the bottom (search for `EDIT ME`).
One entry = one card:

```js
{ name:'PuttQuest', icon:'⛳️', desc:'8-bit minigolf for iOS.', url:'', accent:'#4ade80', tag:'iOS GAME' },
```

- **`url: ''`** (empty) shows the card with a gold **SOON** badge and no link.
  As soon as you paste a real URL (App Store link, deployed site, whatever), the card goes live.
- **`accent`** is the card's hover-glow colour, **`icon`** is any emoji.
- Cards 1–9 automatically get keyboard shortcuts.
- **Multiple platforms on one card** (like Badoku): give it a `menu` array *instead of* `url`,
  and clicking the card opens a chooser:

```js
menu:[
  { label:'iOS',     icon:'🍎', hint:'coming soon',      url:'' },
  { label:'Android', icon:'🤖', hint:'download the APK', url:'https://…' },
],
```

  Menu items with `url:''` show a "coming soon" toast instead of linking.

Other things you might want to change:

- **Email + timezone** — the `CONFIG` object right below `SITES`.
- **Tagline** — search for `G'day 👋` in the HTML.

## Putting it on goatyler.com

Any static host works. Three good free options:

### Option A — Cloudflare Pages (recommended)
1. Go to [pages.cloudflare.com](https://pages.cloudflare.com) → Create project → **Direct upload** → drag this folder in.
2. In the project: **Custom domains → Add → goatyler.com** and follow the DNS prompt
   (easiest if your domain's nameservers are on Cloudflare; it sets the records for you).

### Option B — Netlify Drop (fastest)
1. Drag this folder onto [app.netlify.com/drop](https://app.netlify.com/drop).
2. **Domain settings → Add custom domain → goatyler.com**, then add the DNS records it shows you at your registrar.

### Option C — GitHub Pages
1. Push this folder to a repo, enable **Settings → Pages** (deploy from branch).
2. The `CNAME` file is already here; at your registrar point `goatyler.com`
   A records to GitHub Pages IPs (`185.199.108.153` … `.111.153`) and `www` CNAME to `<user>.github.io`.

All three give you HTTPS automatically.

## Easter eggs (yes, they're features)

- Click the goat → it bleats (with sound). Click it 5 times → 🐐🌧️
- `/` or `⌘K` → command palette
- `1`–`9` → jump straight to a card
