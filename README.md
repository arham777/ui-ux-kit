<div align="center">

# 🎨 UI Design Skill

**Design any web or app interface with a taste-first, anti-AI-slop workflow — then leave behind a `DESIGN_SYSTEM.md` that keeps every future page consistent.**

A portable [Agent Skill](https://skills.sh) for Claude Code, Cursor, OpenAI Codex, Google Antigravity, and any agent that reads the open `SKILL.md` format.

</div>

---

## What it is

`ui-design-skill` is an agent skill that turns a vague design brief into an intentional, brand-specific interface — and stops your AI agent from producing the generic, templated "AI slop" look (purple gradients, Inter everywhere, left-text/right-image hero, sparkle eyebrows, low-contrast gray text).

It does this with a **routed, taste-first workflow** and a **countable anti-slop gate** — "generic" is turned into binary checks the agent must pass before it calls the work done. Every run ends by writing a project-level `DESIGN_SYSTEM.md` so the *next* page matches the last one.

It works for every surface: **landing/marketing, dashboard/admin, app/product UI, e-commerce/store, content/docs, mobile/native, redesigns, and standalone design systems.**

## Why it's different

Most "make it look good" prompts say *"be premium, not generic."* This skill **operationalizes** that:

- 🎯 **Routes the brief to the right rules.** A dashboard and a landing page get different rules — not one recipe for everything.
- 🧪 **Forces one distinctive concept** before building, and checks it landed with an **adversarial self-review** ("cover the brand name — could this be any competitor?").
- ✅ **A countable pre-flight gate.** Hard bans + countable limits the agent must verify against the output, not vibe-check. Catches the exact slop tells: reflex hero splits, sparkle/AI eyebrows, `:focus` rings on mouse click, off-screen tooltips, gray-on-white text, raw `#000`/`#fff`, nested cards, and more.
- 🎨 **Real design fundamentals.** OKLCH color with a 60/30/10 strategy, computed WCAG contrast, depth-over-borders separation, personality-driven typography, full interaction-state sets, and a nine-lever performance budget (Core Web Vitals).
- 📐 **Pulls real references.** Grounds the design in award-winning work instead of the model's averaged defaults.
- 📄 **Leaves a living design system.** A single `DESIGN_SYSTEM.md` source of truth so the whole project stays visually consistent over time.
- ♿ **Accessibility is a floor, not an afterthought** — focus-visible, ARIA patterns, keyboard nav, contrast, reduced-motion, RTL.

## What's inside

```
ui-design-skill/
├── SKILL.md                          # The always-loaded core: routing + laws + workflow + gate
└── references/                       # Loaded on demand, per step (token-efficient)
    ├── surface-rules.md              # Per-surface rules: landing, dashboard, app, mobile, store, docs
    ├── quality-floor.md              # Contrast math, icons, images, a11y floor, perf levers, font table
    ├── experiential.md               # 3D / WebGL / physics tier (only if the brief needs it)
    ├── component-libraries.md        # Capability → library cheatsheet
    └── DESIGN_SYSTEM.template.md      # The deliverable template the skill fills in
```

Only `SKILL.md` is always in context; the heavier references load only when the relevant step needs them.

---

## Installation

> Replace `yourusername/ui-design-skill` with your actual GitHub repo, and the skills.sh slug with your published slug.

### ⚡ Quick install — any supported agent (recommended)

The [skills.sh](https://skills.sh) CLI detects your installed agents and places the skill in the right location for each:

```bash
npx skills add yourusername/ui-design-skill
```

### Claude Code

Claude Code supports the `SKILL.md` format natively.

**User-level (available in every project):**
```bash
git clone https://github.com/yourusername/ui-design-skill.git ~/.claude/skills/ui-design-skill
```

**Project-level (only this repo):**
```bash
git clone https://github.com/yourusername/ui-design-skill.git .claude/skills/ui-design-skill
```

Then invoke it with `/ui-design-skill`, or just describe a design task and it auto-triggers.

### Cursor

Cursor reads project rules and `AGENTS.md`. Add the skill as a project rule:

```bash
git clone https://github.com/yourusername/ui-design-skill.git .cursor/ui-design-skill
```

Then create `.cursor/rules/ui-design-skill.mdc` pointing the agent at it:

```md
---
description: Use the UI Design Skill for any UI/design task
alwaysApply: false
---
When designing, building, redesigning, or auditing any interface, follow
`.cursor/ui-design-skill/SKILL.md` and its `references/` files.
```

(Or run the `npx skills add` command above — it writes this for you.)

### OpenAI Codex

Codex reads `AGENTS.md`. Clone the skill into the repo and reference it:

```bash
git clone https://github.com/yourusername/ui-design-skill.git ./ui-design-skill
```

Add to your `AGENTS.md`:

```md
## Design tasks
For any UI/design work, follow `./ui-design-skill/SKILL.md` and its `references/` files
(routing → concept → build → adversarial review → DESIGN_SYSTEM.md).
```

### Google Antigravity

Antigravity reads `AGENTS.md` / workflow context, same as above:

```bash
git clone https://github.com/yourusername/ui-design-skill.git ./ui-design-skill
```

Reference `./ui-design-skill/SKILL.md` from your `AGENTS.md` or a workflow file so the agent loads it on design tasks.

### Any other agent (generic)

The skill is plain Markdown with YAML frontmatter — no runtime, no dependencies. Any agent that can read a file as context can use it: point the agent at `SKILL.md` and let it open the `references/` files on demand.

---

## How to use

Once installed, trigger it by **slash command** (`/ui-design-skill` in Claude Code) or simply by **describing the task** — the skill auto-triggers on phrases like:

- `"design a landing page for <brand>"`
- `"build a dashboard / store / docs site / mobile app"`
- `"redesign this"` · `"make the UI look premium"` · `"clean up the design"`
- `"create a design system"` · `"audit the UX"`
- `"find design references"` · `"improve performance / Core Web Vitals"`

Mentioning a **brand, color palette, mood, fonts, animation level, card style, framework, or platform** sharpens the result — the more you give, the fewer questions it asks.

## How it works

```
Step 1  Route        → read the brief, pick the surface profile, load its rules
Step 2  Clarify      → ask only the genuine gaps (often zero)
Step 2.5–2.7         → generate assets, pull real references, commit to ONE concept
Step 3  Taste        → OKLCH color, contrast, typography, states, motion
Step 4  Build        → tokens first, modular components, performance levers
Step 4.5 Adversarial → attack your own work; prove it's generic; fix what fails
Step 5  Document     → write DESIGN_SYSTEM.md (the living source of truth)
Verify               → typecheck · compute contrast · render-check the hero · final gate
```

## What you get

Every full design or redesign produces a **`DESIGN_SYSTEM.md`** at your project root with the *actual values used* — real OKLCH/hex, real fonts, component specs, the design concept, the anti-slop gate, and the per-surface rules. Future pages reference this one file so the whole product stays consistent instead of drifting.

## Optional integrations

The skill works standalone, but will use these if available in your agent:
- **Web search / browser** — to pull real design references and render-verify the hero (highly recommended).
- **Image generation** (`/chatgpt-image-gen`, `/ai-image-generation`) — for real assets instead of placeholders.
- **`/ponytail`** — for lean, simplest-thing-that-works implementations.

None are required; the skill degrades gracefully and tells you when it does.

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, adapt the references to your stack.
