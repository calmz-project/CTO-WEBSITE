# $CTO — The Power of Community

The website for **$CTO** (Community Take Over), a community meme token on BNB Chain.

- CA `0x41b68a48446522de90d5dc590a595a2aceb42b66`
- Telegram `t.me/COMMUNITY1455` · X `@CTO_BNB`

## What's in here

```
index.html            the whole site — one self-contained file
assets/img/logo.png    the token logo (favicon, nav, meme cards)
.nojekyll              tells GitHub Pages to serve files as-is
```

No build step, no framework. It loads fonts from Google Fonts and pulls
live figures from the public DexScreener API in the browser. Everything
else is inline.

## Editing content (no coding)

Open **`index.html`** and find the `CONFIG` object near the bottom (inside
`<script>`). Everything the team changes lives there:

| Field | What it does |
|---|---|
| `contract`, `telegram`, `twitter`, `buyUrl`, `chartUrl`, `lockUrl` | Links used across the page. `lockUrl` is the PinkSale liquidity-lock record. |
| `lockLabel` | Lock duration text (currently `"12 months"`). |
| `supply`, `tax`, `maxWallet` | The hero spec panel + tokenomics section. Currently `1,000,000,000`, `3 / 3`, `3%`. |
| `peakFloorMc` | Known all-time-high market cap in USD (`7000`). The displayed ATH ratchets up from here on its own — no editing once the price beats it. |
| `startMc` | Market cap the live "N&times;" multiple is measured from (`100`). |
| `launchTs` | Pool-creation time in ms — powers "days lit". |
| `seed` | Fallback on-chain figures shown before the live API responds, or if it's unreachable. Refresh occasionally so it stays believable. |
| `lines` | Meme Forge starter lines. A shuffled slice shows for each visitor — add your own freely. |

Headlines and body copy are plain HTML — edit them directly in `index.html`.

## Live on-chain figures

The "On Chain" band fetches `api.dexscreener.com` every 30s and shows price,
market cap, liquidity, 24h volume, 24h buys/sells and days since launch,
plus a live multiple vs. the $100 start. If the API can't be reached it
falls back to the `CONFIG.seed` values with a "sample figures" note.

## Deploy (GitHub Pages)

This repo is **private** — GitHub Pages only serves from a private repo on a
paid plan. Either make the repo public (Settings → General → Change
visibility) or keep a paid plan.

1. **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main` / `/`
   (root) → **Save**. Live at `https://calmz-project.github.io/CTO-WEBSITE/`
   in ~1 minute.
2. **Custom domain:** Settings → Pages → *Custom domain*, enter the domain,
   Save (creates a `CNAME` file). Then at your registrar:
   - apex (`yourdomain.com`): four `A` records →
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `www`: a `CNAME` record → `calmz-project.github.io`
3. Tick **Enforce HTTPS** once the certificate is issued.

## Disclaimer

Community project. Nothing on the site is financial advice.
