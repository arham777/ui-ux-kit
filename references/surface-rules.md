# Surface-specific rules

Load this file when Step 1 routes the brief to a surface profile, and apply **only
your profile's section** (a hybrid brief loads two). These rules sit *on top of* the
shared design laws in SKILL.md — they never replace them. Each section ends with its
own pre-flight gate; run it alongside the universal gate in SKILL.md.

---

## B1. Landing / Marketing — page anatomy & conversion flow

A high-converting page is a deliberate sequence. Build this canonical flow (drop any
that don't apply, keep the order):

1. **Navbar** — logo/wordmark, links, one primary CTA. Sticky or reveal; condenses to
   a menu on mobile (single line on desktop, ≤80px tall).
2. **Hero** — see the hero rules below.
3. **Trust bar** — client/partner logos (logos only), stats.
4. **Problem → solution** — name the pain, then the resolution.
5. **Features** — reusable cards, consistent icons and layout.
6. **Product showcase** — real visual depth (mockup/screenshot, not a div fake).
7. **Benefits** — outcome-focused, distinct from features.
8. **Social proof** — testimonials (≤3 lines, real attribution), ratings.
9. **Final conversion** — pricing and/or a focused CTA section.
10. **Footer** — navigation, brand, legal, social.

### Hero — the highest-leverage section (spend disproportionate effort here)

Most visitors judge the whole product in the first second, on the hero alone. Treat
it as the flagship: **iterate it harder and longer than anything else.** Draft it
against 2–3 distinct compositions, pick the one that best lands the Step 2.7 concept,
then refine type, spacing, visual, and one striking move until it earns the scroll.
The hero also sets the design vocabulary (palette, type, motion, depth) every section
below inherits — **a strong hero pulls the whole page up; a weak one drags it down.**
Don't move on until the hero would survive the adversarial review on its own.

Three hard requirements:
1. **Contained in the first viewport — verified by *height*, not just width.** Navbar +
   entire hero (eyebrow, headline, sub, CTAs, visual) fit inside `100svh` at real
   laptop heights (**test ~700px and ~800px**, not only 1280px wide). Use `min-h-svh`
   (not `h-screen`/`100vh`). If it doesn't fit, scale the headline via `clamp()` keyed
   to `min(vw, vh)`, shorten copy, or tighten spacing — never let headline/CTAs spill
   below the fold.
2. **Centered on both axes** (`min-h-svh grid place-items-center` or flex
   `items-center`), safe padding — not top-aligned with whitespace dumped below, and
   **no empty full-width band/spacer above the hero** pushing the content off-center.
   This is render-only: confirm by screenshot at ~700/800px (see SKILL.md "Verify before
   done"), not by reading the code.
3. **Composition: the left-text / right-image split is the DEFAULT FAIL.** It is the most
   templated hero on the web, and "I made it slightly distinctive" is not a pass — that
   escape hatch is what lets the slop through. **Start from a non-split composition:** (a)
   centered editorial; (b) oversized typographic (headline *is* the art); (c) full-bleed
   image/video with AA-legible scrim; (d) asymmetric/off-grid. Use the split **only** if you
   can write the one specific move that earns it (asymmetric ratio, image bleeds off the
   edge, an overlap/depth or motion move) — and a plain 50/50 text-left + rounded
   image-card-right is never that move. Land one striking move regardless of composition.

Headline ≤2 lines on desktop (count them); one supporting line (≤20 words);
primary + secondary CTA; max 4 text elements; "trusted by" logos move *below* the hero.

### Conversion & sections
- One primary goal per page; exactly **one primary CTA style** reused everywhere;
  secondary CTAs quieter; repeat the primary CTA at hero, mid-page, and final section.
- Full-screen sections use `min-height` (never fixed `height`), content centered both
  axes, everything fits at every breakpoint — reflow/rescale within the type scale.
  Verify widths (375 / 768 / 1280+) **and** heights (~700 / ~800).

### Horizontal card rails — NEVER a raw native scrollbar
Choose by intent: row moves *as the page scrolls* → **scroll-pinned**; browse on
demand (drag/arrows) → **snap carousel**. Ambiguous long page → scroll-pinned for a
hero showcase, snap carousel for secondary rails.

**Snap carousel (default — the user browses). Each step prevents a specific bug:**
1. **Kill the phantom vertical scrollbar.** `overflow-x:auto` forces the cross axis
   from `visible` to `auto`, so the track gains `overflow-y:auto` and throws a vertical
   bar the moment content is slightly taller. **Set `overflow-y:hidden` explicitly.**
2. **Hide the bar cross-browser:** `scrollbar-width:none` (FF), `-ms-overflow-style:none`,
   `::-webkit-scrollbar{display:none}`. Keep the track focusable.
3. **Fade the edges:** `mask-image: linear-gradient(to right, transparent, #000 var(--fade), #000 calc(100% - var(--fade)), transparent)`.
4. **Snap flush:** `scroll-snap-type:x mandatory` on the track, `scroll-snap-align:start`
   on each card, `scroll-padding-inline` matching the gutter.
5. **Controls:** visible prev/next (≥44px) calling `el.scrollBy({left, behavior:"smooth"})`
   — instant (`behavior:"auto"`) under `prefers-reduced-motion` — plus drag/swipe and a
   position indicator (dots, never color alone).
6. **A11y:** `role="region"` + `aria-label`; `aria-hidden` on offscreen cards; no
   autoplay by default.

**Scroll-pinned (long pages only).** GSAP ScrollTrigger `pin:true` + `x` translate with
`scrub` (pin at `top top`), or Framer `useScroll`+`useTransform`. See `/gsap-scrolltrigger`.

**Both, always:** animate `x`/`transform` (never `scrollLeft` loops); no visible OS
scrollbar (incl. phantom vertical); faded edges; smooth easing; reduced-motion falls
back to a clean vertical stack or tap-through, never a raw horizontal scrollbar.

### B1 gate
Hero fits at ~700–800px heights (nothing below the fold); hero vertically centered with no
empty band above it; headline ≤2 lines; composition is NOT a plain left-text/right-image
split (default fail) — any split has a written distinctive move; no sparkle/AI icon or
vague-tagline eyebrow; primary CTA repeats ≥2×; full-screen sections fit at 375/768/1280 widths
**and** ~700/800 heights; ≥3 different section layout families; eyebrows ≤ ceil(sections÷3);
consecutive zigzag splits ≤2.

---

## B2. Dashboard / Admin / Data

- **Density over drama.** No forced full-viewport hero. Information breathes via spacing
  and grouping, not boxes — cards **only** where elevation conveys real hierarchy;
  otherwise group with negative space / token dividers.
- Keep the full interaction-state set, but motion is restrained and functional.

### Tables
- Sortable with `aria-sort` reflecting current state; readable row rhythm; sparse
  dividers; **tabular/monospaced numerals** for columns, prices, timers.
- Virtualize lists at **50+ rows**. Sticky header on long tables. Right-align numbers,
  left-align text. Row hover + selected states (background, not border). Empty, loading
  (skeleton rows), and error states for every table.
- Bulk actions: select-all + per-row checkboxes, a visible action bar, confirm
  destructive, **undo** where possible.

### Charts (match type to data; never decorate over clarity)
- **Type → data:** trend → line/area; comparison → bar; proportion → pie/donut **≤5
  slices** (else bar); distribution → histogram; relationship → scatter; part-to-whole
  over time → stacked area.
- **Never color alone:** add direct labels, patterns/textures, or shapes so series are
  distinguishable for colorblind users; avoid red/green-only pairs.
- **Legends & tooltips:** legend near the chart (not below a fold); tooltips/data labels
  on hover (web) and tap (mobile, ≥44pt targets) showing exact values; legends
  clickable to toggle series.
- **Axes:** label with units; readable, auto-skipping ticks on small screens; locale-aware
  number/date/currency formatting; clear time granularity (day/week/month) with switching.
- **Contrast:** data marks ≥3:1 vs background; data text labels ≥4.5:1; gridlines
  low-contrast (~gray-200) so they don't compete with data.
- **Every chart designs four states:** empty ("No data yet" + guidance, not a blank
  axis frame), loading (skeleton/shimmer, not an empty frame), error (message + retry),
  and loaded. Entrance animation respects `prefers-reduced-motion`; data readable
  immediately.
- **Scale:** 1000+ points → aggregate/sample with drill-down, don't render all.
- **Accessibility:** provide a data-table alternative or `aria-label`/text summary of the
  chart's key insight; interactive points/bars keyboard-navigable; tooltips
  keyboard-reachable (not hover-only).
- **Restraint:** emphasize the trend over decoration; avoid heavy gradients/shadows that
  obscure data; offer CSV/image export for data-heavy products.

### B2 gate
Cards only where elevation is real; numerals tabular; lists 50+ virtualized; every
table and chart has empty/loading/error; no color-only meaning in charts; data marks
≥3:1 and data text ≥4.5:1.

---

## B3. App / Product UI

### Navigation (consistent, predictable, one level of truth)
- **Placement is identical across every screen** — never change nav by page type.
  Current location visually marked (color/weight/indicator). One primary action per
  screen; secondary actions visually subordinate.
- **Don't mix patterns at the same level** — not tab + sidebar + bottom nav together.
  Primary nav (tabs/bottom bar) and secondary nav (drawer/settings) stay clearly
  separated. Large screens (≥1024px) prefer a sidebar; small screens use bottom/top nav.
- **Back is predictable:** preserves scroll position, filters, and input; never silently
  resets the stack or jumps home. Support system gesture nav (iOS swipe-back, Android
  predictive back) without conflict.
- **Reachability:** every key screen deep-linkable via URL; core nav reachable from deep
  pages (don't fully hide it in sub-flows); breadcrumbs for 3+ level web hierarchies;
  search easily reachable with recent/suggested queries.
- **Items:** icon **+** text label (icon-only harms discoverability); overflow/more menu
  when actions exceed space; badges sparingly, cleared after visit; destructive actions
  (delete, logout) visually + spatially separated from normal items.
- **Modals are not navigation** — they break the path; use them for focused tasks only.
  On route change, move focus to the main content region for screen readers.

### Forms & flows
- Full shared-laws forms rules, plus multi-step progress indicators, autosave on long
  forms, confirm-before-destructive, undo where possible.
- **Every view ships empty / loading / error states** — this is where products feel
  unfinished. Design all three.

### B3 gate
Every data view has all three states; one primary action per screen; nav placement
constant across screens; back restores state; no mixed nav patterns at one level.

---

## B4. Mobile / Native (iOS / Android / React Native / Flutter)

> **Scope note.** This skill's engine is web-first (tokens, CSS depth, the carousel/perf
> rules). For true native, the section below is **platform-idiom guidance layered on top**
> — navigation, touch, safe areas, modality, keyboard. It does **not** replace the depth of
> Apple HIG / Material 3 on platform components, state restoration, or framework specifics;
> for those, follow the cited standard and the platform's own component library
> (`references/component-libraries.md` mobile rows). On RN/Flutter the token + state +
> a11y laws still apply; the literal CSS mechanisms don't.

Apply platform idioms; cite the standard (Apple HIG / Material).
- **Pick one platform feel** and stay coherent — don't mix iOS and Android carelessly.
- **Touch targets ≥44×44pt (iOS) / 48×48dp (Android)**, ≥8pt spacing; expand hit area
  for small icons. No hover-only interactions; tap feedback within ~100ms.
- **Safe areas:** keep primary controls clear of notch, Dynamic Island, gesture bar,
  edges. Reserve space for status/nav bars.
- **Navigation:** iOS bottom Tab Bar / Android Top App Bar for top level; bottom nav ≤5
  items with icon + label; predictable back preserving scroll/state; deep-linkable key
  screens. **List → detail** is the core pattern: tappable rows, push transition, back
  restores list position.
- **Modality — sheets, not desktop modals.** Bottom sheets (detents) for contextual
  actions/pickers; full-screen cover for focused tasks; action sheets for choices;
  center alerts only for confirms/destructive. Every sheet is swipe-to-dismiss **and**
  has a visible close.
- **Keyboard avoidance (most-missed bug):** focused field stays visible above the
  keyboard; correct keyboard/input type per field (email, number, tel). Never let the
  keyboard cover the field being typed into.
- **Gestures & feedback:** pull-to-refresh on feeds, swipe actions on rows (with a
  visible non-gesture fallback), edge-swipe back on iOS. Light haptics on key actions;
  visual tap feedback within ~100ms. Never make a gesture the *only* way to an action.
- **Type & motion:** support Dynamic Type / system text scaling without truncation;
  prefer spring/physics curves; respect reduced-motion.
- **Prefer native/system controls**; customize only when branding requires.

### B4 gate
Touch targets ≥44/48; safe areas respected; bottom nav ≤5; no hover-only or
gesture-only interaction; keyboard never covers the focused field; Dynamic Type doesn't
break layout.

---

## B5. E-commerce / Store

Convention-heavy — surprise on look, never on flow.
- **Listing / category:** consistent product-card grid (image, name, price, one signal
  like rating or badge — not five). Faceted filters in a left rail (desktop) / bottom
  sheet (mobile); each active filter a removable chip; result count + sort always
  visible; filtering updates the URL (shareable, back-safe). Paginate or infinite-scroll
  deliberately — if infinite, keep a reachable footer and restore scroll on back.
- **Product detail (PDP):** gallery with real images (zoom on desktop, swipe on mobile,
  never a div mock); price + variant selectors with **out-of-stock shown, not hidden**;
  quantity; one high-emphasis **Add to cart**; stock/shipping/returns as concrete trust
  facts. Variant changes update price, image, and availability together.
- **Cart & checkout:** cart shows line items, editable quantities, itemized total **with
  shipping/tax resolved before the final step** (no surprise totals). Checkout is short,
  linear, progress-marked; **guest checkout offered**; one primary action per step; never
  lose entered data on error; inline-validate payment fields; confirm before placing the
  order; explicit order-confirmation state.
- **Trust & states:** real reviews with attribution; security/returns signals near the
  buy action; design empty cart, empty search/filter results, sold-out, and payment-error
  states.

### B5 gate
PDP shows price + variants + stock (out-of-stock visible); totals resolved before final
step; guest checkout offered; empty-cart / no-results / sold-out / payment-error states
designed.

---

## B6. Content / Editorial / Docs

Legibility and wayfinding, not theatrics.
- **Reading measure & rhythm:** body 16–20px, **line length 60–75ch** (never full-bleed
  prose), line-height ~1.6–1.7; generous paragraph spacing; limited heading hierarchy
  (h2/h3 inside articles). Optimize for sustained reading, not first-scroll impact.
- **Wayfinding:** sticky/section TOC with active-section highlight on long pages;
  breadcrumbs for docs; prev/next at article end; visible reading position welcome,
  decorative parallax not.
- **Prose elements, all styled deliberately:** blockquotes, inline code, **code blocks
  (mono, syntax-highlighted, copy button, horizontal scroll without a raw native bar)**,
  figures with captions, tables, callout/admonition boxes, footnotes. None fall back to
  browser defaults.
- **Docs specifics:** persistent left nav (collapsible, current page marked),
  version/search affordance, anchored headings with copyable links, keyboard-navigable
  search.
- Restrained motion; no full-viewport hero theatrics; the content is the design.

### B6 gate
Prose at 60–75ch; TOC/nav with active state on long pages; code blocks styled (mono,
highlight, copy, no raw scrollbar); no full-bleed marketing hero on a reading surface.
