---
name: prd-writer
description: "Turns a validated idea into a short, sharp PRD that ends in a ready-to-run vibe-code prompt for the V1 MVP. Use this as stage 4 of the Product OS pipeline, after idea-validator returns GO (and after rubric-builder, if the project needed one). Trigger on 'write the PRD', 'spec this out', 'turn this into a build', 'what are we building', or any point where a validated idea is ready to become a buildable V1. This skill defines WHAT the V1 is, WHY, for WHOM, and hands off a build prompt an engineer, designer, or vibe-coding tool can act on. It does not build the product (that's vibe-coding) and does not validate the idea (that's stage 2). The PRD is not final until the review panel has pressure-tested it."
---

# PRD Writer

Stage 4 of the pipeline. Takes the validated idea and produces a **1-pager PRD that ends in a vibe-code prompt** for the V1 MVP — the way AI PMs work now: the PRD isn't a long document that gets handed off and separately translated into a build; it *is* the thing that produces the build instruction, sharp enough that an engineer, a designer, or a vibe-coding tool can act on it and give feedback.

This skill absorbs what used to be separate scoping and design steps. It decides the V1 cut and gives just enough design direction to build from — all inside one short document.

Write it against **five quality bars** (adapted from Lenny's "great PRD"):
1. **Problem-oriented** — crystallize the problem in a few strong sentences near the top, so every reader points the same direction.
2. **Clear success criteria** — define specifically what "shipped and working" means, so tradeoffs can be judged against it.
3. **Just enough direction** — give requirements and constraints without over-specifying the solution; leave room for engineers and designers to find better answers.
4. **Urgency** — include a proposed timeline to review, build, and ship, to prevent scope explosion.
5. **Short and sweet** — it's a 1-pager. Push extra context to an appendix. Clean up formatting whenever it gets messy.

## Step 1: Read the upstream artifacts — don't re-derive

Read `problem.md`, `validation.md`, and (if it exists) the rubric file, plus the CLAUDE.md scope. These already contain the problem, the user, the build intent, the verdict, and any locked scope. Pull from them; don't re-ask. In particular:

- Carry forward the **build intent** (portfolio / internal / commercial) — it sets the success bar.
- Carry forward any **carry-into-PRD items** validation.md flagged (e.g. "make the differentiation visible," "record the commercial-pull gap honestly"). These are assignments, not optional.
- Respect the **locked MVP scope** in CLAUDE.md. If the PRD would exceed it, stop and ask.

## Step 2: Clarify before writing

Ask the user 3–5 targeted questions only about what the upstream artifacts *don't* already answer — usually the V1 cut and the shape of the build. For example: which single flow is the core demo? what's explicitly deferred? seeded/simulated or live? For anything still unknown, use `[NEED: ...]` rather than guessing.

## Step 3: Decide the V1 cut (absorbed scoping)

Name the smallest version that proves the core value. Everything not essential to the hypothesis goes to a "not in V1" list with a one-line reason. This is where scope discipline lives — be ruthless. A V1 that demos the core "aha" in one flow beats a fuller one that ships later.

## Step 4: Write the PRD (the 1-pager)

Keep it to roughly one page. Use this structure:

```markdown
# PRD — [Product / feature name] (V1)

## Problem
[2-3 strong sentences from problem.md. Who struggles with what, and why it matters. No solution yet.]

## Who it's for
[The one specific user from problem.md, and the goal they're chasing.]

## What V1 is
[The solution in plain English — what the user can do. Describe the experience, not the tech. A few sentences.]

## The core flow (the demo)
[The single most important user journey, step by step. This is what gets built and shown. Foreground whatever makes the value *visible* — per any validation.md note.]

## In V1 / Not in V1
**In:** [the must-haves that prove the core value]
**Not in:** [explicitly deferred, each with a one-line why]

## Success criteria
[What "shipped and working" means, calibrated to the build intent. For a portfolio piece: the demo shows [what judgment] convincingly and a viewer gets it in under a minute. Be specific.]

## Key decisions & tradeoffs
[2-4 real choices, each: "chose X over Y because Z, accepting [cost]." Where product judgment shows.]

## Known limits & honest gaps
[Anything validation.md told the PRD to address honestly — e.g. commercial-pull gap. Don't gloss.]

## Proposed timeline
[Rough: review/align by [when], build by [when], demo by [when]. Keeps scope from exploding.]

## Appendix (optional)
[Extra context that would otherwise bloat the 1-pager.]
```

## Step 5: The vibe-code prompt (the payload)

After the 1-pager, produce a clean, self-contained prompt an engineer, designer, or vibe-coding tool (Claude Code, Lovable, v0) can run to build V1. This is the skill's signature output. It must be copy-pasteable and stand on its own.

### Ground the design in real references (so V1 doesn't look generically AI-generated)

Default AI-generated UI looks generic. Grounding the build in real, shipped design patterns makes V1 look designed. Offer the user a tiered choice — free by default, paid only if they want automation:

**Free default (no subscription — recommended):** Point the user to a free UI-reference gallery and have them pick 2-3 real screens matching what they're building, then feed those patterns into the vibe-code prompt. Good free galleries:
- **Collect UI** and **UXArchive** — real app screens organized by pattern (onboarding, sign-up, dashboards, empty states).
- **Pttrns** — mobile design patterns by category.
- **Land-book** — landing pages, if V1 has a marketing/landing surface.
The manual step (user browses, picks, describes) replaces the automated pull — same grounding benefit, zero cost.

**Optional automation (only if the user already has it):**
- **VP0** — a free, AI-readable iOS design library; you paste a link and the build tool rebuilds from it. Free, but verify it fits the target platform (it's iOS-focused).
- **Mobbin MCP** — pulls real reference screens live inside Claude Code, but requires a **paid Mobbin account**. Only suggest if the user says they have it; never assume, and never make it a requirement.

**Ask the user once:** "Want to ground the design in real references? Free way: browse a gallery like Collect UI, pick 2-3 screens you like, and I'll build the prompt around those patterns. Or if you have Mobbin MCP / VP0 connected, we can pull references automatically."

**However references are gathered, the rule is the same — extract patterns, never clone.** The vibe-code prompt should instruct the build tool to (1) look at the 2-3 references, (2) **write a short breakdown of the underlying patterns first — hierarchy, spacing, interaction, information density — before any UI code**, then (3) design original UI from those principles. That breakdown step is the difference between grounded design and brand-mimicry. If the user skips references entirely, fall back to plain design direction — the skill must work fully without any of these tools.


```markdown
## Vibe-code prompt — V1 MVP

**Build this:** [one-sentence what we're building]

**Context:** [the user + the problem, 2 sentences, so the tool understands the "why"]

**The core flow to build:**
[The screens/steps from "The core flow" above, concretely. What the user sees and does, screen by screen.]

**Must include (V1):**
- [each must-have as a build instruction]

**Do NOT build (out of scope):**
- [each deferred item — this keeps the tool from over-building]

**Data:** [seeded/simulated vs live — name exactly what's mocked and what's real]

**Design direction:** [just enough — tone, key layout intent, what to foreground. Not pixel specs; leave room for good design choices. If the user gathered real references (free gallery, VP0, or Mobbin): instruct the tool to write a short pattern breakdown from those references FIRST — hierarchy, spacing, interaction — then design original UI from those principles, never cloning. If no references: give plain design direction only.]

**Definition of done:** [when this prompt has succeeded — the user can [do the core thing] end to end.]
```

Keep the prompt tight. It should give direction without dictating every detail — the same "just enough" bar as the PRD.

## Step 6: Run the review panel — the PRD is not final until this passes

Before the PRD is approved, pressure-test it through the panel (defined in CLAUDE.md). Each reviews through one lens only and returns concerns:

- **AI Engineer** — is the vibe-code prompt actually buildable as written? What's ambiguous or missing? Edge cases?
- **AI Product Designer** — is the core flow coherent? Where would the user get confused? Does the demo foreground the value?
- **Skeptic** — what untested assumptions does this rest on? What could make the V1 fall flat? (Address any commercial-pull / differentiation-visibility gaps validation.md flagged — honestly, not glossed.)
- **Customer** — would the target user actually get the value from this flow? In the first minute?
- **SME (only if the problem is in a specialized industry)** — grounded in research, not assumed expertise. Skip for general-consumer products.

Present the panel's concerns to the user. The user decides what to act on; revise the PRD and prompt accordingly. Only then is the PRD final.

## Check in before finalizing

Share the 1-pager, the vibe prompt, and the panel's concerns with the user conversationally. Ask what they want to act on before writing the final `PRD.md`. Only write the file once they confirm.

## Anti-patterns

- Never write a long PRD. It's a 1-pager; extra context goes to the appendix.
- Never re-derive the problem, user, or intent — pull them from the upstream files.
- Never let the vibe-code prompt over-specify or under-specify: just enough direction.
- Never skip the "Do NOT build" list in the prompt — it's what stops the tool over-building.
- Never gloss a gap validation.md told you to address honestly.
- Never mark the PRD final before the panel has reviewed it.
- Never instruct the build to clone or copy design references (from any source). Extract patterns, design original UI.
- Never make paid tools (like Mobbin) a requirement — default to free references; the skill must work fully without any paid tool.
- Never exceed the locked MVP scope without asking.
- Never fill a field with a guess. Use `[NEED: ...]`.

## Rules

- Five bars, always: problem-oriented, clear success criteria, just-enough direction, urgency, short.
- The PRD's signature output is a runnable vibe-code prompt for V1 — that's the handoff.
- Calibrate success criteria to the build intent from problem.md.
- The panel is mandatory. A PRD the panel hasn't seen is a draft, not a PRD.
- Ruthless on scope: the smallest V1 that makes the value visible wins.

## Exit checklist

- [ ] Problem, user, and intent pulled from upstream files, not re-derived
- [ ] V1 cut is explicit, with a "Not in V1" list
- [ ] Success criteria are specific and calibrated to build intent
- [ ] The 1-pager is actually ~one page
- [ ] A clean, copy-pasteable vibe-code prompt for V1 exists
- [ ] The prompt has a "Do NOT build" list and a data (seeded/live) note
- [ ] The review panel has run and its concerns were addressed or consciously accepted
- [ ] `PRD.md` written with no unfilled `[...]`

## Handoff

When `PRD.md` (1-pager + vibe prompt) is final and the user approves it, the next stage is **vibe-coding (stage 5)** — it takes the vibe-code prompt and builds V1. Tell the user that's next and wait for them to start it. Do not start building automatically.