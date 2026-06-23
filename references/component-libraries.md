# Component libraries & registries — cheatsheet

> **Examples, not facts.** This list reflects a knowledge cutoff and the ecosystem
> moves fast. Use it only as the **fallback** when no live source is available, and
> confirm a name still exists / is maintained before installing it. The reliable
> order is always: **(1) use what `package.json` already has → (2) MCP / WebSearch
> for the current best option → (3) verify → (4) only then these names.** Select by
> *capability* (what you need), then resolve the package; capabilities don't go
> stale, names do.
>
> To keep this current, edit this file — the skill's logic lives in `SKILL.md` and
> does not need to change when names do.

## Capability → example libraries (by surface / need)

| Capability you need | Example libraries (verify before use) | Notes |
|---|---|---|
| Product / app / dashboard you own the code | **shadcn/ui** (Radix primitives under the hood) | The default. Copy-in components; re-theme radii/color/shadow/type — never ship the stock look. |
| Bulletproof a11y + full custom visuals (headless/unstyled) | **Radix Primitives**, **React Aria** (Adobe), **Ark UI**, **Headless UI**, **Base UI** (MUI) | This is the layer the ARIA rules map onto — use it instead of a `div`+onClick widget. |
| Speed over a bespoke look (opinionated kits) | **Mantine**, **Chakra UI**, **MUI** (Material), **Ant Design** (enterprise/data-dense) | Heavier to de-template. Still re-theme tokens to the project. |
| Marketing / landing flourishes (animated sections) | **Aceternity UI**, **Magic UI**, **Tailwind UI / Catalyst** | Starting points, not final — strip default gradients & demo copy; re-skin to tokens. |
| Component discovery / registry | **21st.dev** (shadcn-registry compatible; has an MCP), shadcn registries, **Origin UI**, **HyperUI**, **Flowbite**, **DaisyUI** | Pull individual components into a shadcn-style setup; de-template each. |
| Charts / data viz | **Tremor** (Tailwind dashboards), **Recharts** (simple React), **visx** (low-level custom), **Nivo**, **ECharts** (heavy), **Chart.js** | Match library weight to need; apply the dashboard chart rules (color-not-alone; empty/loading/error states). |
| Mobile — iOS | **SwiftUI** built-ins (+ SF Symbols) | Prefer platform-native controls (see B4). |
| Mobile — Android | **Jetpack Compose** + **Material 3** | Prefer platform-native controls. |
| Mobile — React Native | **Tamagui**, **React Native Paper** (Material), **NativeWind** | — |
| Mobile — Flutter | **Material** / **Cupertino** widgets | — |

## Official design systems (use the real package when the brief reads as one)

See the "Honesty rule" table in `SKILL.md`: Fluent UI, Material 3
(`@material/web`), Carbon (`@carbon/react`), Primer (`@primer/react`),
`govuk-frontend` / `uswds`, shadcn/ui, Tailwind v4. One system per project; never
import its tokens then override 90%.

## Guardrails (always apply — these don't change)

- One primary styled base per project; mix only the headless-primitive layer beneath it.
- Never ship a library's default theme — re-map to the project tokens first.
- Registry/marketing components are scaffolding: pass the category-reflex test (1e)
  and concept test (Step 2.7) before they count as done.
- Use an accessible primitive instead of hand-rolling ARIA.
- Don't pull a whole library for what native HTML/CSS or an installed dep does
  (ponytail ladder).
