# DESIGN_SYSTEM.md

> The official design reference for this project. Every future page, section,
> component, and UI update must follow this file so the design stays consistent.
> **Replace every placeholder and every italic guidance line with the actual
> values you used** — real hex/OKLCH codes, real font names, real component specs.
> The descriptive prose in this template is instruction, not content: do not ship
> it verbatim. A section left with template wording is an incomplete section.
> Delete this blockquote when done.

---

## 1. Project overview

- **Website / product name:**
- **Website type:** (landing page, dashboard, store, portfolio…)
- **Surface profile:** (Landing/Marketing · Dashboard/Admin · App/Product UI ·
  E-commerce/Store · Content/Editorial/Docs · Mobile/Native · Redesign ·
  Design-system-only) — so future work routes the same.
- **Platform:** (web · iOS · Android · cross-platform)
- **Target users:**
- **Main design goal:**

## 2. Brand direction

- **Visual style:** (minimal, warm, bold, editorial…)
- **Mood & tone:**
- **Design personality:**
- **Design concept (one sentence — the Step 2.7 commitment):** the single
  distinctive organizing idea and how it shows up in layout / type / color /
  motion. Must not describe any competitor equally well.
- **Adversarial-review verdict:** the concept-test result from Step 4.5 (cover the
  brand name — is this still distinctive?) and the one weakness found + fixed.
- **Reference style used:** the 3–5 references pulled (Awwwards / Dribbble /
  Mobbin / etc.) with links, and the specific move adapted from each. (If web
  research was unavailable, note that and list the named exemplars reasoned from.)
- **Voice & UX copy:** the writing voice (e.g. plain/confident, warm, technical),
  CTA verb style (one label per intent), and the rules for empty/error/loading
  copy. No generic filler ("Elevate / Seamless / Acme / Lorem ipsum"); real or
  honestly-marked mock data only.

## 3. Color system

Map every color to its role. Use only these values across the project.

| Role | Color | Hex | Usage |
|---|---|---|---|
| 60% — Dominant | | | Page backgrounds, large surfaces |
| 30% — Secondary | | | Raised sections, cards, supporting blocks |
| 10% — Accent | | | Buttons, links, highlights, focus rings |

**Usage rules** for backgrounds, text, buttons, borders, cards, and highlights:
- Backgrounds:
- Text:
- Buttons:
- Cards:
- Highlights / focus:
- Separation: background contrast + shadow only — **never borders**.
- **Dark mode (if shipped):** semantic tokens themed (not raw-hex inversion);
  tinted near-black base, surfaces raised by +lightness, accent chroma lowered;
  every text pair re-verified for AA in dark separately.

## 4. Typography system

Define the scale ONCE; every text references a named step (no inline sizes).

- **Brand personality (drives the font choice):** (corporate-clean, editorial-
  luxury, warm-human, bold-loud, playful/funky/cartoon, minimal-swiss, brutalist-
  technical, elegant-fashion)
- **Font family / pairing:** (heading + body; max 2 families + optional 1 mono)
- **Why these fonts fit the personality:** (one line — the type alone should
  signal the right vibe; a playful brand is not on a corporate grotesque)
- **Type scale (named steps + exact values):** display, h1, h2, h3, body-lg,
  body, body-sm, caption, button — with their mobile→desktop sizes (`clamp()` or
  per-breakpoint).
- **Body text:** (size; never below 16px)
- **Line-height / line-length:** (~1.5 body; ~60–75ch)
- **Button text style:**
- **Responsive rules:** scaling lives in the scale itself; headings scale down on
  mobile; never clip hero text; never truncate on mobile.

## 5. Layout system

- **Container widths:**
- **Section spacing:**
- **Grid rules:**
- **Page anatomy / section order:** the canonical sequence of sections for the
  main page(s) (e.g. navbar → hero → trust → problem/solution → features →
  showcase → benefits → social proof → conversion → footer).
- **Conversion / CTA flow:** primary goal, primary vs secondary CTA style, where
  the primary CTA repeats.
- **Surface-specific flows (fill in for your profile):** Store → listing/filter,
  PDP, cart, checkout steps, trust placement. Content/Docs → reading measure, TOC/
  nav, code-block & prose treatment. Mobile → sheets/modality, keyboard avoidance,
  list→detail, gestures, safe areas. (Skip the rows that don't apply.)
- **Hero composition:** which hero pattern was used (centered editorial /
  oversized-typographic / full-bleed image / asymmetric / distinctive split) and
  the one striking move it lands. The hero fits `100svh` at laptop heights
  (~700–800px), is centered on both axes, and the headline is ≤2 lines on desktop.
- **Full-screen sections:** each major section uses `min-height` (not fixed
  height), fills the viewport, and centers its content vertically + horizontally
  — every element fits inside the section with safe padding, nothing clipped or
  overflowing, verified at each breakpoint **by width (375/768/1280) and height
  (~700/800)**.
- **Horizontal card rails / scroll section(s):** which rails or pinned sections
  scroll horizontally; pattern used (snap carousel vs scroll-pinned); how driven
  (transforms, GSAP/Framer/Embla). **No native scrollbars** — snap + smooth +
  prev/next controls; reduced-motion falls back to a vertical stack or tap-through.
- **Mobile-first behavior:**
- **Breakpoints:** mobile (~375px), tablet (~768px), desktop (~1280px+).
- **Alignment rules:**

## 6. Component system

Each component is defined once and reused. Document the spec for each:

- **Component base / library:** (e.g. shadcn/ui + Radix primitives, Mantine, MUI,
  headless via React Aria, or native CSS) — **one base per project**, re-themed to
  the tokens above (never the library's default look). Note any registry sources
  used (21st.dev / Aceternity / Magic UI) and that each was de-templated.
- **Chart / data-viz library (if any):** (Tremor / Recharts / visx / Nivo / ECharts)
- **Buttons:** (variants, sizes, states)
- **Cards:**
- **Badges:**
- **Navbar:**
- **Footer:**
- **Forms:**
- **Inputs:**
- **Feature sections:**
- **CTA sections:**

## 7. Card & section style

- **Chosen style:** (borderless / rounded / bento / flat / soft shadow / other)
- **Radius:**
- **Shadow / elevation:**
- **Gradients:** where used, direction, and the exact palette stops (no
  purple/blue-purple unless approved).
- **Glassmorphism:** where used (e.g. sticky nav, hero card), blur amount, and
  surface translucency.
- **Rule:** no nested card-heavy layouts; one elevation hierarchy only.

## 8. Icon system

- **Icon library:** (not Lucide by default)
- **Icon size:**
- **Icon color:**
- **Usage rules:** icon-only controls have accessible labels.

## 9. Image & asset rules

- **Logo:** type (AI-generated / web image / text wordmark) and **format (SVG or
  PNG, transparent, high-res).**
- **User-provided images:**
- **AI-generated images:**
- **Stock images:** (source, e.g. Unsplash)
- **Crop style:**
- **Radius:**
- **Visual treatment:**

## 10. Animation & interaction system

- **Animation library:** (GSAP + ScrollTrigger / Framer Motion / CSS-only)
- **Hover states:**
- **Section reveal behavior:**
- **Horizontal-scroll behavior:** how rails/pinned sections are driven
  (transform-based, snap, prev/next + drag). Required hygiene: `overflow-y:hidden`
  (no phantom vertical bar), scrollbars hidden cross-browser, `mask-image` edge
  fade (no hard cut), `scroll-snap` + `scroll-padding` flush to gutter,
  `role="region"` + dots, no autoplay by default. Never a raw native scrollbar.
- **Button interaction:**
- **Cursor pointer rules:**
- **Interaction states (every interactive element):** default / hover / focus /
  **active-pressed** / disabled — specs for each.
- **Async feedback:** loading state pattern (button "…" label + spinner /
  skeleton) and the success/error result pattern.
- **Toast / inline message system:** component, position, durations, success vs
  error styling (paired with icon/label, never color alone).
- **Form feedback:** inline validation, error/success messages, required markers,
  helper text.
- **Data view states:** empty, loading, and error states for every data view.
- **Reduced-motion support:** respect `prefers-reduced-motion` (horizontal
  section falls back to vertical stacking).
- **Performance (Core Web Vitals — target LCP < 2.5s, CLS < 0.1, INP < 200ms):**
  animate only `transform`/`opacity`; code-split by route + ship less JS; critical
  CSS first, defer the rest; lazy-load below-the-fold images/components (hero/LCP
  image prioritized); every image/media has `width`/`height` or `aspect-ratio`;
  modern formats (WebP/AVIF) + responsive `srcset`; `display: swap` fonts; protect
  the main thread (debounce/throttle, off-thread heavy work); smart caching
  (hashed assets + long cache headers, CDN, static/ISR, SWR for data).

### Experience tier — 3D / WebGL system (fill in only if Experiential tier)

- **Experience tier:** Standard (DOM + CSS/GSAP/Framer) or Experiential (3D/WebGL).
- **3D / WebGL library:** (Three.js / React-Three-Fiber + drei)
- **Shaders:** list of GLSL materials/effects and where they're used.
- **Physics engine:** (Rapier / Cannon-es / Matter.js) and what it drives.
- **Smooth scroll:** (Lenis / Locomotive) and how it syncs to ScrollTrigger.
- **Page transitions:** (Barba.js / view transitions) — behavior.
- **Spline / Lottie:** where embedded.
- **3D asset pipeline:** formats (glTF/GLB), compression (Draco/Meshopt), where
  loaded, code-splitting strategy.
- **Performance budget:** target fps, draw-call/texture limits, offscreen pause.
- **Fallbacks:** mobile/low-power degrade path, no-WebGL fallback, and the
  `prefers-reduced-motion` static equivalent.
- **Accessibility:** canvas alternative content, keyboard/focus handling, no
  copy baked into the canvas, reserved dimensions (no layout shift).

## 11. Accessibility rules

- **Contrast rules:** body/supporting text ≥ 4.5:1, large text/UI ≥ 3:1, computed
  (not eyeballed); no light-gray-on-white copy; re-verified per theme.
- **Focus states:** visible `:focus-visible` on every interactive element; never
  removed without replacement.
- **Keyboard navigation:** full operation, tab order = visual order, skip-to-content
  link, modals trap + restore focus.
- **Semantics & ARIA:** semantic elements + landmarks; composite widgets (tabs,
  combobox, menu, dialog, accordion) follow WAI-ARIA Authoring Practices; form
  errors associated via `aria-describedby` + announced.
- **System adaptation:** `prefers-reduced-motion`, `forced-colors`/High-Contrast,
  text scaling + 200% zoom, RTL via logical properties (if localized).
- **Text readability:**
- Never rely on color alone — pair with icon or label.

## 12. Anti-AI-slop rules

The **canonical countable gate lives in `SKILL.md` → "Pre-flight check"** (hard bans,
countable limits, performance gates) plus your profile's gate in
`references/surface-rules.md`. That is the single source of truth — run it against the
output before shipping any page; it is not restated here so the two can't drift apart.

Record below only what's **specific to this project** (so a future page can be checked
against the same decisions the gate was applied to):

- **Approved palette (the only colors allowed):** _list every hex/OKLCH from §3._
- **Pure `#000`/`#fff` used?** _No by default — or, if yes, name the concept that
  justifies it (brutalist / hard editorial / true-OLED) so it reads as deliberate._
- **Concept-test verdict (from §2):** _cover the brand name — still distinctive? + the
  one weakness found and fixed._
- **Project-specific exceptions to the gate:** _any rule the brief deliberately overrides,
  with the reason — so it isn't later "fixed" by mistake._

## 13. Future page instructions

Every future page must reuse the same colors, typography, spacing, components,
icons, cards, animation rules, and image style documented above. Do not
introduce a new visual style unless the user explicitly updates this file.

## 14. Update policy

If colors, typography, components, animations, cards, icons, or image style
change later, update this file immediately so it never drifts from the live UI.
