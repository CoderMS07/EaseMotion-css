# Advanced Mega Menu Navigation

1. **What does this do?**
   Renders a multi-column dropdown navigation panel for top-level menu items, with categorized link groups, icons, "New"/"Beta" badges, a featured promo card, and a primary CTA button — animated with a fade + scale + slide transition, and collapsing into an inline accordion on mobile.

2. **How is it used?**
   Wrap the whole bar in `.megamenu-bar`, with `.megamenu-nav` holding the menu items. A top-level item that should open a panel is `.megamenu-item` containing a `.megamenu-trigger` button and a `.megamenu-panel`; the panel holds `.megamenu-panel-inner` with one or more `.megamenu-col` blocks (each with a `.megamenu-col-title` and a list of `.megamenu-link`s), optionally followed by a `.megamenu-feature-card` for a promo/featured slot. Plain items with no panel just use `.megamenu-plain-link`. Toggling `.megamenu-item-open` on the `.megamenu-item` (done via the included JS on click, or could be wired to `:focus-within`) reveals the panel. On small screens, `.megamenu-mobile-toggle` reveals `.megamenu-nav-open` on the nav, and panels switch from floating overlays to inline accordions automatically via the included media query.

3. **Why is this useful?**
   EaseMotion CSS currently has no navigation component built for content-heavy sites — SaaS marketing pages, docs portals, and admin tools all eventually need more than a flat dropdown. This submission packages a full mega-menu pattern (columns, badges, icon links, a featured card, responsive collapse, and `prefers-reduced-motion` support) as a single composable example, consistent with the framework's CSS-only, animation-forward philosophy. The small amount of vanilla JS included is only for toggling open/closed state and the mobile hamburger — no external libraries or frameworks are used, and the panel transitions themselves are pure CSS.

### Notes for the maintainer
- Class names are intentionally unprefixed (`megamenu-*`) per the contribution guidelines — happy to see these renamed to `ease-*` on integration.
- The desktop panel uses `position: absolute` + opacity/transform for the open transition; mobile swaps to a `max-height` accordion transition at the `860px` breakpoint, since animating to `auto` height isn't natively supported by CSS transitions.
- `prefers-reduced-motion: reduce` disables all transitions on the panel, chevron, and nav links.
- Tested in Chrome, Firefox, and Edge. The icons in this demo are plain Unicode glyphs (no icon font/CDN) to keep the file fully self-contained — these would likely be swapped for SVGs or an icon set already used elsewhere in EaseMotion CSS during integration.