# CTO Website

Marketing site for **$CTO** (Community Take Over), a community token on BNB Chain.

Live: <https://ctobnb.website>

| | |
|---|---|
| Contract | `0x41b68a48446522de90d5dc590a595a2aceb42b66` |
| Telegram | <https://t.me/COMMUNITY1455> |
| X | <https://x.com/CTO_BNB> |

## Stack

A single static HTML file. No build step, no framework, nothing to install.
Fonts are loaded from Google Fonts. On-chain figures are fetched in the browser
from the public DexScreener API. Everything else (markup, styles, script) is
inline in `index.html`.

## Structure

| Path | Purpose |
|---|---|
| `index.html` | The entire site. |
| `assets/img/logo.png` | Logo used for the favicon, nav, and generated meme cards. |
| `CNAME` | Custom domain for GitHub Pages. |
| `.nojekyll` | Disables Jekyll processing on GitHub Pages. |

## Local development

Serve the directory with any static file server, for example:

```bash
npx serve
# or
python -m http.server
```

Then open the address it prints.

## Configuration

All editable values are in the `CONFIG` object near the bottom of `index.html`.

| Key | Purpose |
|---|---|
| `contract`, `telegram`, `twitter`, `buyUrl`, `chartUrl`, `lockUrl` | Links used across the page. `lockUrl` points to the PinkSale liquidity-lock record. |
| `lockLabel` | Lock duration shown in the UI (`"12 months"`). |
| `supply`, `tax`, `maxWallet` | Values in the hero spec panel and tokenomics section. |
| `peakFloorMc` | Known all-time-high market cap in USD. The displayed ATH is a client-side high-water mark seeded from this value and climbs on its own; it does not need editing after the price beats it. |
| `startMc` | Market cap the live multiple (`N×`) is measured against. |
| `launchTs` | Pool-creation timestamp in milliseconds. Drives "days lit". |
| `seed` | Fallback on-chain figures shown before the live API responds or if it is unreachable. |
| `lines` | Starter lines for the meme-card generator. A shuffled subset is shown per visitor. |

Headlines and body copy are plain HTML in the same file.

## On-chain data

The "On Chain" section polls `api.dexscreener.com` every 30 seconds for price,
market cap, liquidity, 24h volume, 24h buy/sell counts, and days since the pool
was created. If the request fails, `CONFIG.seed` is displayed with a
"sample figures" note. All values fall back to `CONFIG.seed` on first paint so
the section is never blank.

## Theme

Light and dark. By default the theme follows the visitor's local clock (light
between 07:00 and 19:00, dark otherwise). Using the toggle overrides that for
8 hours, after which the clock resumes.

## Deployment

GitHub Pages serves the `main` branch from the repository root. Any push to
`main` redeploys automatically, typically within a minute.

Custom domain `ctobnb.website` (apex and `www`). DNS records at the registrar:

- Apex (`@`): four `A` records to `185.199.108.153`, `185.199.109.153`,
  `185.199.110.153`, `185.199.111.153`
- `www`: `CNAME` to `calmz-project.github.io`

The `CNAME` file pins the domain. HTTPS is enforced in **Settings → Pages**.

## License

Community project. Nothing on this site is financial advice.
