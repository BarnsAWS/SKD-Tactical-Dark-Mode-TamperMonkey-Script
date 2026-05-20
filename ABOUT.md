# About This Repository

## Purpose

This repository delivers a Tampermonkey userscript that re-themes the SKD Tactical retail storefront at `https://skdtac.com` using the AWS Cloudscape "Polaris Dark Mode" token palette.

## Design Principles

- **Cloudscape palette as ground truth.** Surfaces, text tiers, links, borders, focus rings, and primary actions all use Cloudscape v3.3 tokens (`#161d26` body, `#1b232d` cards, `#0a0f15` inset controls, `#42b4ff` link/accent, `#ff9900` primary CTA). No hand-picked hex values. See `STANDARDS.md`.
- **Two-layer architecture.** CSS injected at `document-start` for an immediate dark paint; JS surface-enforcement passes as the safety net for inline styles, runtime injections, framework gradients, and shadow roots.
- **Hands off media + brand imagery.** Product photos, hero images, video previews, and brand logos are excluded from color overrides.
- **Hands off the cascade.** No `filter: invert(1)`. Brand colors and semantic alerts are preserved.

## Script Architecture

`skd_tactical_dark_mode.user.js` runs in seven phases (see `STANDARDS.md` for the full reference): framework hook → CSS injection at `document-start` → JS `enforceDarkSurfaces()` pass → top-bar detection → inline control + selected row passes → tight-loop style observer → main mutation observer + load-time safety net.

## Why This Repository Exists

Retail storefronts ship light-only themes that fatigue the eyes during late browsing sessions. This script delivers a single, predictable, Cloudscape-aligned dark experience for SKD Tactical without altering product photography or brand identity.

## Maintenance Notes

- Keep the userscript at the repository root so the GitHub raw URL is the canonical Tampermonkey install link.
- Cloudscape tokens are the source of truth. If Cloudscape revises the dark palette, update the constants block at the top of the userscript and `STANDARDS.md`.
- Validate after any storefront redesign or platform migration.

## Source References

- `STANDARDS.md` — the Cloudscape-aligned dark-mode standard this script implements.
- `SANITIZATION.md` — sanitization log for this repository.
- AWS Cloudscape Design System: <https://cloudscape.design>

## License

MIT (see `LICENSE`).
