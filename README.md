# DEPRECATED — superseded by the Web Dark Mode Bundle

> ⚠️ **This standalone userscript is deprecated as of v2.0 of the bundle.**
>
> All sites previously covered by this repo (and 10 others) are now consolidated into a single auto-updating Tampermonkey userscript:
>
> **https://github.com/BarnsAWS/Web-Dark-Mode-Bundle**
>
> Direct install URL:
>
> `https://raw.githubusercontent.com/BarnsAWS/Web-Dark-Mode-Bundle/main/web_dark_mode_bundle.user.js`
>
> ## Migration
>
> 1. Open Tampermonkey dashboard.
> 2. **Disable or remove** this script (otherwise two scripts will fight on the same page).
> 3. Open the install URL above and click **Install**.
> 4. Tampermonkey will auto-update from `main` going forward.
>
> ## Why the bundle exists
>
> - One install, one auto-update across all covered sites.
> - Shared Cloudscape v3.3 engine — every site gets the same standard at the same time.
> - Adding a new site is a one-file change to `SITES` in the bundle.
>
> The original README/ABOUT and userscript are retained below this notice for archival / reference.
>
> ---

# SKD Tactical Dark Mode TamperMonkey Script

A Tampermonkey/Violentmonkey userscript that applies an AWS Cloudscape-aligned dark theme to the SKD Tactical retail storefront at `https://skdtac.com`.

## What This Repository Contains

- `skd_tactical_dark_mode.user.js` — the Tampermonkey userscript.
- `STANDARDS.md` — the Cloudscape-aligned dark-mode standard the script implements.
- `SANITIZATION.md` — what was scrubbed before this repo was made public.
- `LICENSE` — MIT.
- `README.md`, `ABOUT.md`.

## Behavior Coverage

The script follows the **Cloudscape Dark Mode Standard v3.3** (see `STANDARDS.md`):

- Forces a Cloudscape "Polaris Dark Mode" palette across the SKD Tactical surface — top header, primary navigation, search input, hero / promo banners, category browse, product listing grid, product detail page, buy box, cart, checkout, account, order history, and footer.
- Preserves the full Cloudscape text hierarchy (emphasis → heading → body → muted → disabled).
- Applies semantic alert tints (red error, blue info, green success) and Amazon Orange (`#ff9900`) to primary action buttons.
- Forces dark surfaces on dropdowns, popovers, modals, menus, listboxes, tooltips.
- Runs the v3.3 `enforceDarkSurfaces()` JS pass which detects light surfaces via *both* `background-color` and `background-image` (so framework gradients with white stops are stripped), and routes them by luminance bucket to `--bg-secondary` (`#1b232d`) or `--bg-tertiary` (`#232b37`).
- Includes the v3.3 sub-component coverage block so card-internal `header` / `[class*="title"]` / `[class*="body"]` / `[class*="content"]` / `[class*="footer"]` drop to transparent and inherit the parent card surface.
- Attaches the v3.3 tight-loop `MutationObserver` on `style` attribute mutations, batched via `requestAnimationFrame`, so framework writes during interaction (focus, blur, hover, async cart updates, lazy-loaded grid pages) get corrected within ~16 ms.
- Includes the v3.1 inline-control rule so search inputs and any quantity/option selects render as inset wells with a `#656871` border (passes WCAG 1.4.11).
- Includes the v3.2 generalized in-content selected rule so the active filter / sort / pagination state gets a `#001129` background with a 3 px `#42b4ff` left-rail.
- Pierces open shadow roots and re-applies the same stylesheet.
- **Hands off product images, video previews, and SVG icons** so product photography renders correctly. Brand logos and decorative iconography keep their original colors.

## Install on Chrome

1. Install Tampermonkey: <https://chromewebstore.google.com/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo>
2. Open the Tampermonkey dashboard and confirm it is enabled.
3. Open the raw userscript URL and let Tampermonkey prompt for install:
   `https://raw.githubusercontent.com/BarnsAWS/SKD-Tactical-Dark-Mode-TamperMonkey-Script/main/skd_tactical_dark_mode.user.js`
4. Click **Install**.
5. Visit `https://skdtac.com` and refresh once.

## Install on Firefox

1. Install Tampermonkey: <https://addons.mozilla.org/en-US/firefox/addon/tampermonkey/>
2. Open the Tampermonkey dashboard.
3. Open the raw userscript URL above and click **Install**.
4. Visit `https://skdtac.com` and refresh once.

## Verification Checklist

- [ ] Page body and main content render on `#161d26`.
- [ ] Top header and primary nav render dark with readable nav labels.
- [ ] Search input renders as an inset `#0a0f15` well with a `#656871` border.
- [ ] Product grid tiles render on `#1b232d` cards with `#424650` borders.
- [ ] Product photos and brand logos keep their original colors.
- [ ] Primary CTAs (Add to Cart, Continue Checkout) render in Amazon Orange `#ff9900` with dark text.
- [ ] No card sub-component renders with a light surface.
- [ ] No element renders with a `background-image: linear-gradient(white, ...)`.
- [ ] No bright white flash on initial load.

## Troubleshooting

- **Bright sections after load** — hard refresh (Ctrl+F5) and confirm Tampermonkey is enabled.
- **Embedded iframe still light** — Tampermonkey does not inject into cross-origin iframes by default.

## Relationship to SKD Tactical

This is an unofficial, community-maintained client-side userscript. It is not affiliated with, endorsed by, or sponsored by SKD Tactical. The script alters the visual presentation in your own browser only and does not modify any server-side content.

## Source References

- `STANDARDS.md` — the Cloudscape-aligned dark-mode standard.
- `SANITIZATION.md` — sanitization log.
- AWS Cloudscape Design System: <https://cloudscape.design>

## License

MIT (see `LICENSE`).
