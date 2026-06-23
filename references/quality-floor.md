# Quality floor — depth detail for Steps 3 & 4

The core (`SKILL.md`) carries the *laws*; this file carries the *detail* behind them.
Load it when you reach Step 3 (taste) and Step 4 (build) and apply the relevant
sections. Nothing here overrides a core law — it expands it.

---

## Contrast — the computation (referenced from SKILL.md "Text contrast")

Verify by computing, not by eye, in light and dark separately:
1. Linearize each sRGB channel: `c ≤ 0.03928 ? c/12.92 : ((c+0.055)/1.055)^2.4`.
2. Relative luminance: `L = 0.2126R + 0.7152G + 0.0722B`.
3. Ratio: `(L_lighter + 0.05) / (L_darker + 0.05)`.

Run it in a one-off script, or reuse a token pair you already verified. Don't assert
"passes AA" without the number. **Fast pre-check** (a screen, not a substitute): body
and bg must differ by ≥45 in OKLCH lightness; smaller almost certainly fails.

---

## Typography — personality → category → face lookup (Move B from SKILL.md)

Pick the row that fits *this* brief's nuance; write one line tying the face to the
personality. (The Move A→C method and the anti-reflex rule stay in the core.)

| Personality | Category | Heading options | Body |
|---|---|---|---|
| Corporate-clean / modern SaaS | Grotesque sans | Geist, Hanken Grotesk, Mona Sans, Neue Montreal, Space Grotesk | same family, weight contrast |
| Editorial / luxury / heritage | High-contrast serif | Fraunces, Bodoni Moda, Playfair Display, Editorial New, Cormorant | clean sans or readable serif |
| Warm / friendly / human | Humanist sans / soft serif | Epilogue, Schibsted Grotesk, Bricolage Grotesque, Young Serif | Mulish, Nunito Sans |
| Bold / loud / sporty | Heavy / condensed display | Anton, Archivo Expanded, Clash Display, Hatton, Monument Extended | neutral grotesque |
| Playful / funky / cartoon / kids | Rounded / quirky display | Fredoka, Baloo 2, Lilita One, Chewy, Bagel Fat One, Gluten | rounded sans — Nunito, Rubik, Quicksand |
| Minimal / swiss / rational | Neutral grotesque | Basis/Diatype/Suisse-like, Inter *(genuinely neutral brief only)* | same family, weight contrast |
| Brutalist / technical / dev | Mono + plain grotesque | Space Mono, JetBrains Mono, IBM Plex Mono, Departure Mono | IBM Plex Sans, Untitled-Sans-like |
| Elegant / fashion / feminine | Ligature display serif | Canela-like, Reckless, Saol, Ivypresto | light sans (Jost, Calmetta) |

---

## Surface treatment — gradients & glass (tasteful, on-brand)

- **Gradients:** only within the approved palette, low-contrast, directional, on large
  backgrounds or behind the hero. No default purple / blue-purple unless approved. No
  gradient text (`background-clip:text`).
- **Glassmorphism:** sparingly, on genuinely floating elements; `backdrop-blur` +
  translucent surface + one soft shadow, over a backdrop where text behind still meets
  AA. Never glass-on-glass; never decorative-by-default.
- **Depth kit:** soft (hue-tinted) shadows + rounded corners + whitespace, from tokens.
- **Shape consistency:** one corner-radius scale (or a documented rule), everywhere.

---

## Icons

Pick one library and commit. **Don't default to Lucide** — choose for personality:
corporate/SaaS → Phosphor, Heroicons, Radix; editorial/luxury → thin/duotone Phosphor or
custom; warm/playful → Phosphor rounded, Iconoir, hand-drawn; brutalist/dev → Tabler,
custom mono, Material Symbols sharp; mobile → SF Symbols (iOS) / Material Symbols
(Android). Match weight to type weight; size/stroke/color from tokens; icon-only controls
get accessible labels; never emojis as structural icons; never mix two families on one
surface.

---

## Images

Match images to brand and industry; consistent crop, radius, treatment. Real photography
or generated assets over div "fake screenshots." Set width/height (no layout shift); never
decorative-only without `alt` handling.

---

## Accessibility (universal floor)

The core keeps the contrast + focus essentials; this is the full floor — apply it on
every surface.

- **Contrast & focus:** meet ratios (compute them, above); visible `:focus-visible` ≥3:1
  on every interactive element; never `outline:none` without a replacement. (A focus ring
  is a legitimate outline — see the core's note on borders.)
- **Keyboard:** full operation; tab order matches visual order; focus traps only inside
  modals (which restore focus on close).
- **Semantics:** real elements (`button`, `a`, `nav`, `main`…); a skip-to-content link;
  one `h1` then sequential headings.
- **Composite widgets follow WAI-ARIA APG** — tabs, combobox, menu, dialog, accordion,
  listbox, switch, tooltip get their roles/states/arrow-key interaction. Don't hand-roll a
  `div`+onClick where a pattern exists.
- **Forms:** programmatic `<label>`; errors via `aria-describedby` + announced
  (`aria-live`/`role="alert"`); required in text not color; group with `fieldset`/`legend`.
- **State, not color:** pair with icon/text/shape. Support `forced-colors` / Windows High
  Contrast (use `currentColor`/system colors).
- **Motion & scaling:** respect `prefers-reduced-motion`; honor text scaling and 200% zoom.
- **Direction & i18n:** logical properties (`margin-inline`, `inset-inline`) so RTL
  mirrors; leave room for text expansion.
- **Images & media:** descriptive `alt` (empty for decorative); captions/transcripts; no
  autoplay audio.

---

## Performance & delivery — the nine levers (referenced from SKILL.md Step 4)

Target **Core Web Vitals: LCP < 2.5s, CLS < 0.1, INP < 200ms.** These are the goal the
levers serve — state them as "targeted via the levers"; report a measured number only if
you actually measured it. Apply all nine:

1. **Perceived speed** — acknowledge interactions <100ms; optimistic UI + skeletons over
   blocking spinners; render above-the-fold first.
2. **Smaller first load** — code-split by route/feature; tree-shake; defer non-first-paint.
3. **Critical path first** — inline/early critical CSS; defer/`async` non-critical
   CSS/JS/third-party.
4. **Ship less JS** — prefer CSS / RSC / SSR; hydrate only interactive leaves.
5. **Lazy load** — `loading="lazy"` below-fold images; dynamic-import below-fold components
   and animation/3D libs.
6. **Protect the main thread** — <16ms/frame; workers for heavy compute; debounce/throttle
   scroll/resize/input; never drive scroll/mouse through React state (use motion
   values/rAF).
7. **Stable layouts (CLS)** — `width`/`height` or `aspect-ratio` on every image/media/embed;
   reserve space for async content; `font-display: swap` with `size-adjust`.
8. **Optimize images** — WebP/AVIF; `srcset`/`sizes`; correct dimensions; hero/LCP eager,
   rest lazy.
9. **Smart caching** — hashed immutable filenames + long cache; CDN; static/ISR/SSG over
   per-request; SWR/react-query for data.

---

## Honesty — use real design systems when the brief calls for one

Don't hand-recreate a system's CSS. Install the **official** package; don't import its
tokens then override 90%. **One system per project.**

| Brief reads as… | Use |
|---|---|
| Microsoft / enterprise SaaS | Fluent UI (`@fluentui/react-components`) |
| Google-ish / Material | Material 3 (`@material/web`) |
| IBM-style B2B analytics | Carbon (`@carbon/react`) |
| GitHub-style devtool | Primer (`@primer/react`) |
| UK / US public-sector | `govuk-frontend` / `uswds` |
| Modern SaaS you own | shadcn/ui (never ship its default state — customize radii/colors/shadows) |
| Tailwind-based build | Tailwind v4 utilities |

Aesthetics with no official package (glass, bento, brutalism, editorial, dark-tech) →
native CSS + Tailwind, honest about borrowed inspiration. For library/registry selection
(shadcn / Radix / charts / mobile), see `references/component-libraries.md`.
