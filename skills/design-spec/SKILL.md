---
name: design-spec
description: "Runs a real design pass BEFORE an app is built, so the result looks like a product designer shaped it — not a generic AI default. Use this right before the build stage (vibe-coding), whenever a project has a visual interface (a web app, landing page, dashboard, screens a user looks at). Trigger on 'make it look good', 'I want an impressive design', 'design the app', 'design direction', or any point where a PRD/build prompt is ready and the UI is about to be built. This skill produces a full design direction — the design intent and reasoning, a flow/wireframe, real reference screens, a VISUALLY RENDERED mockup of the key screen, and a palette/type system — as 2-3 directions the user chooses from, then writes design.md. It does not build the app (vibe-coding) or fetch product data."
---

# Design Spec

Most AI-built apps look generic because they're built code-first, with design as an afterthought. This skill flips that — a real design pass before any UI code exists. But "a design pass" does NOT mean handing the user a few colors and fonts and asking them to imagine the rest. That is a style tile, not a design direction, and no one can make a real design decision from hex codes alone.

A real design direction shows the *thinking* and shows it *realized*: what the user is feeling, the design intent that answers it, what the flow looks like, a real reference screen that proves the direction, and the key screen actually mocked up so the user can SEE it and react. Palette and type come last, in service of that — not as the whole deliverable.

**This skill produces visual mockups, not descriptions of mockups.** It renders the key screen so the user judges something real. Free tools/references only; patterns extracted, never cloned; the user chooses the direction.

## Step 1: Understand the user's emotional journey, not just the screens

Read the PRD/build prompt and CLAUDE.md scope. For each screen, name two things:
- **What the user is feeling / needing at that moment** (e.g. "overwhelmed, wants to feel this will actually help").
- **The one screen that carries the "wow"** — the emotional payoff. This is where design effort concentrates and what gets fully mocked up.

Design decisions flow from the emotional journey. "The learner arrives overwhelmed" is *why* the design is calm and one-thing-at-a-time — state that logic, don't just assert a "tone."

## Step 2: Research the design intent (the WHY behind any direction)

Before proposing looks, establish the reasoning any direction must serve:
- **Who's the user and what must they feel?** (Trust? Calm? Momentum?) Tie it to the product's purpose.
- **What does this *kind* of product look like when it's done well?** Pull real reference screens from free sources (Mobbin free tier, Land-book, Collect UI, UXArchive, Happy Hues for palette-in-context). Name specific real products/screens, not categories.
- **What's the design principle** each reference demonstrates (hierarchy, restraint, rhythm, the single-hero-number move for a reveal, etc.).

This research is the backbone. A direction without a stated *why* is decoration.

## Step 3: Produce 2-3 FULL directions — each realized, not described

Give the user 2-3 genuinely different directions. Each one is NOT "a palette + fonts." Each includes ALL of:

1. **Design intent (1-2 lines):** the feeling this direction creates and why it fits the user's emotional journey.
2. **Flow / wireframe:** a simple visual layout of the screens — boxes/structure showing where things sit, what's foregrounded, the reading rhythm. Rendered, not just described.
3. **A real reference screen:** "this direction is in the spirit of [real product/screen] — here's the principle we're taking." Concrete and named.
4. **The wow-screen, VISUALLY MOCKED UP:** an actual rendered mockup of the key screen (e.g. the reveal) in this direction — real layout, real type, real color, real content from the PRD. This is the thing the user actually judges.
5. **The system, in service of the above:** palette (real hex — primary, accent, background, surface, text, success/alert), type pairing (free/Google Fonts), spacing feel. Grounded via free generators (Coolors, Khroma, Color Hunt, Adobe Color, Open Color). Contrast checked.

**Render the mockups so the user sees them.** Use the available visual/artifact rendering to show at least the wow-screen for each direction as real UI. If a full render isn't possible, produce a clear rendered wireframe at minimum — never fall back to a plain text list of colors as the deliverable.

Make the 2-3 directions genuinely distinct (different intent, not three shades of one idea) and name each.

## Step 4: Present, recommend, let the user choose

Show the directions side by side — the rendered wow-screen, the intent, the reference, the flow, then the system. Recommend one with a reason tied to the user's goal. The user picks, or mixes ("direction A's layout with B's palette" is fine). Wait for the choice before writing the spec.

## Step 5: Write design.md (the spec the build builds to)

Once chosen, write it concretely:

```markdown
# Design Spec — [product name]

## Design intent
[The feeling and the reasoning — why this direction serves the user's journey.]

## Reference direction
[The real screen(s) this draws from, and the principle taken — patterns, not pixels.]

## Flow
[Screen order and the layout intent of each — what's foregrounded, the rhythm.]

## The wow-screen
[Detailed intent + the mockup reference — how this screen creates the payoff.]

## Palette (chosen: [name])
- Primary / Accent / Background / Surface / Text (primary,secondary) / Success / Alert — with hex.

## Type
- Headings: [font], scale intent. Body: [font].

## Spacing & components
- Base unit, container width, density; button/card/input style (rounded/sharp, filled/bordered, shadow).

## Screen-by-screen intent
- [Each screen: layout + what to foreground. The wow-screen gets the most detail.]

## Build notes
- Accessibility, responsive intent, and the one screen that must feel special.
```

## Anti-patterns

- Never deliver just a palette + fonts and call it a design direction. That's a style tile — show intent, flow, a real reference, and a rendered mockup.
- Never describe a mockup in words when you can render it. The user must SEE the key screen.
- Never propose a look without a stated WHY tied to the user's emotional journey.
- Never clone a reference — extract the principle, design original.
- Never present one option as decided — give 2-3 real, distinct directions.
- Never ship a palette that fails contrast for prettiness.
- Never require paid design tools.

## Rules

- A direction = intent + flow + real reference + rendered wow-screen + system. All five, or it's incomplete.
- Render, don't describe. The user judges something visual.
- Every choice traces back to what the user must feel at that screen.
- The user chooses the look; the skill researches, realizes, and recommends.
- Free tools only. Concentrate effort on the wow-screen.

## Exit checklist

- [ ] User's emotional journey per screen is named, wow-screen identified
- [ ] Design intent (the WHY) researched and stated, with real named references
- [ ] 2-3 genuinely distinct directions, EACH with intent + flow + reference + rendered wow-screen mockup + system
- [ ] The wow-screen is actually rendered visually for each direction, not described
- [ ] Palettes have real hex and pass contrast
- [ ] The user chose (or mixed) a direction
- [ ] design.md written with intent, flow, palette, type, spacing, component, screen intent, build notes

## Handoff

When design.md is written and approved, the next step is **vibe-coding** — it builds the app to this spec (apply design.md, not defaults). Tell the user that's next and wait for them to start it.