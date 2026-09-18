---
name: design-spec
description: "Runs a design pass BEFORE an app is built, so the result looks intentionally designed instead of generically AI-generated. Use this right before the build stage (vibe-coding), whenever a project has a visual interface — a web app, a landing page, a dashboard, screens a user looks at. Trigger on 'make it look good', 'I want an impressive design', 'design the app', 'give me a palette', or any point where a PRD/build prompt is ready and the UI is about to be built. This skill produces a design system (references, patterns, 2-3 palette/style options for the user to choose from, and a spec) that the build then builds TO. It does not build the app (that's vibe-coding) and does not fetch/curate product data."
---

# Design Spec

The reason AI-built apps look generic is they're built code-first, with design as an afterthought — the build tool reaches for its defaults. This skill flips that: it runs a **design pass before any UI code is written**, grounded in real references, and hands the build a concrete design system to build *to*. Design-first, not design-after.

It uses **free tools only** — no paid design software required. And it never clones references: it extracts *patterns* and produces an *original* design system for this product.

The user chooses the final look — this skill presents **2-3 distinct palette/style options** and waits for their pick before finalizing. Design taste is the user's call, not the skill's.

## Step 1: Understand what's being designed

Read the PRD / build prompt and the CLAUDE.md scope. Identify:
- **The screens/surfaces** this app has (e.g. an input/onboarding screen, a data-reveal screen, a list/results screen).
- **The one screen that carries the "wow"** — the emotional center the design budget should favor (e.g. a funnel reveal). Design serves that moment first.
- **The product's tone** — what should it feel like? (trustworthy/calm, energetic/bold, editorial/clean). Pull this from the product's purpose and user, not from thin air.

## Step 2: Pull real references (free sources)

Gather references so the design is grounded in proven patterns, not invented. Point the user to free sources and/or browse them:
- **Layout / UI patterns:** Collect UI, UXArchive, Mobbin (free tier for browsing), Land-book (for landing pages), Happy Hues (palettes shown *in context*).
- **For each key screen**, find 2-3 real examples of that pattern (an onboarding flow, a data-viz/reveal screen, a results list).

Extract, don't collect: for each reference, note *why* it works — the hierarchy (what draws the eye first), spacing/density, and interaction pattern. Write this as a short pattern breakdown. **Never copy a reference's exact look** — the breakdown feeds an original design, it is not a template.

## Step 3: Build 2-3 palette/style options (free tools)

Produce **2-3 distinct, complete style directions** for the user to choose from. Each option is a real, usable mini design-system, not a vibe:

For each option, specify:
- **Palette** — real hex codes: a primary, a secondary/accent, a background, a surface, text colors, and a success/alert color. Use free generators to ground these (Coolors, Khroma, Color Hunt, Adobe Color) and/or a developer-ready system (Open Color, Material). Check contrast is legible (WCAG-ish) — a pretty palette that fails on readability is a fail.
- **Type** — a heading font + body font pairing (free/Google Fonts), and the scale intent (big confident headings vs. compact).
- **Feel in one line** — e.g. "calm, editorial, trustworthy" vs. "bold, high-energy, product-y."
- **Where it shines** — how this option would treat the wow-screen specifically.

Make the 2-3 options *genuinely different* (not three shades of the same blue) so the choice is real. Give each a short name.

## Step 4: Present and let the user choose

Show the user the 2-3 options plainly — palette swatches (as hex + description), fonts, feel, and how each handles the wow-screen. Recommend one with a reason, but the choice is theirs. Wait for their pick (or their mix — "option 2's palette with option 1's type" is fine). Do not proceed to the spec until they choose.

## Step 5: Write design.md (the spec the build builds to)

Once the user picks, write the chosen direction as a concrete spec:

```markdown
# Design Spec — [product name]

## Feel
[One or two lines — the intended feel and tone.]

## Palette (chosen: [option name])
- Primary: #......
- Accent: #......
- Background: #......
- Surface: #......
- Text (primary / secondary): #...... / #......
- Success / Alert: #...... / #......

## Type
- Headings: [font], [scale intent]
- Body: [font]

## Spacing & layout
- [Base spacing unit, container width intent, density — compact vs airy.]

## Component style
- [Buttons, cards, inputs — rounded vs sharp, bordered vs filled, shadow use.]

## Screen-by-screen intent
- [Screen]: [layout intent, what to foreground]
- [The wow-screen]: [extra detail — this is where polish concentrates]

## Reference patterns applied
[Short: which real patterns informed this, and the principle taken from each. No cloning — principles only.]

## Build notes
[Anything the build must honor — accessibility, responsive intent, the one screen that must feel special.]
```

## Hand-off to the build

The build stage (vibe-coding) builds *to* this `design.md` — palette, type, spacing, and component style are inputs, not afterthoughts. Tell the build explicitly: "apply design.md; don't use default styling." That instruction is what makes the difference between designed and generic.

## Anti-patterns

- Never build the UI here — this skill produces the design system; the build applies it.
- Never clone a reference's exact look. Extract patterns, design original.
- Never present one option as a fait accompli — give the user 2-3 real choices.
- Never ship a palette that fails contrast/legibility for the sake of prettiness.
- Never make the 2-3 options near-identical — they must be genuinely different to be a real choice.
- Never require paid design tools — free sources only.

## Rules

- Design-first: the system is decided before any UI code is written.
- Grounded in real references, but always original — patterns in, not pixels.
- The user chooses the look; the skill informs and recommends.
- Free tools only.
- Concentrate polish on the one screen that carries the product's "wow."

## Exit checklist

- [ ] Screens identified, including the wow-screen
- [ ] Real references pulled and their patterns broken down (not cloned)
- [ ] 2-3 genuinely distinct style options presented with real hex palettes
- [ ] The user chose (or mixed) a direction
- [ ] design.md written with concrete palette, type, spacing, component style, and screen intent
- [ ] Contrast/legibility checked
- [ ] Hand-off tells the build to apply design.md over defaults

## Handoff

When `design.md` is written and the user approves it, the next step is **vibe-coding** — it builds the app to this spec. Tell the user that's next and wait for them to start it. The build must apply design.md rather than default styling.