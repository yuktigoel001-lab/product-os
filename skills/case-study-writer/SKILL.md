---
name: case-study-writer
description: "Turns a shipped product and its pipeline artifacts into a public 'how this was built' story — the kind people actually read and share on LinkedIn or a blog. Use this as the final stage of the Product OS pipeline, after a product is built and working. Trigger on 'write the case study', 'write up how I built this', 'the build story', 'turn this into a post', or any point where a shipped product needs its story told publicly. This skill writes the narrative; it does not build or change the product. It reads the pipeline's own artifacts (problem, validation, PRD, design, the build) so the story is grounded in what actually happened, not invented."
---

# Case Study Writer

The final stage. Turns a shipped product into a public build story — a "how I built this" piece for LinkedIn, a blog, or a portfolio. This is a specific genre with its own rules, and it is NOT a dry project report. A project report lists what was made; a build story makes a stranger care, teaches them something, and lets the builder's judgment show through the telling.

Read the pipeline's artifacts first (problem.md, validation.md, PRD, design.md, and the build/README) so every claim is grounded in what actually happened. Never invent decisions, numbers, or dead-ends — pull the real ones.

## What makes a public build story work (the genre rules)

1. **Lead with the tension, not the product.** Open on the problem or a moment of friction the reader recognizes ("I was drowning in newsletters"), never "X is a tool that…". The reader needs a reason to care in the first two lines.
2. **Tell the messy middle honestly.** The decisions, the trade-offs, the near-misses, the thing that almost went wrong. Honesty is what makes it credible and human instead of a brag. A story with no struggle reads as fake.
3. **Teach one transferable lesson.** People share build stories that taught them something they can use ("validate before building," "run a fake-door test"). Find the real lessons in what the builder actually did.
4. **Let the capability be implicit.** The quality of the thinking does the selling. Never say "hire me" or "look how skilled I am" — show the judgment, let the reader conclude it.
5. **Make it skimmable.** Headers, short paragraphs, one idea each. Assume it's read on a phone between meetings.

## Step 1: Mine the artifacts for the real story

Read across the pipeline artifacts and pull out:
- **The genuine problem** and why it mattered to the builder (from problem.md).
- **The sharp decisions** — where the builder made a non-obvious call and why (merging ideas, cutting scope, choosing prototype over live, a validation verdict, a design trade-off). These are the spine of the story.
- **The near-misses and honest moments** — a bug caught in QA, an idea that got killed, a scope that had to shrink, an assumption that was wrong. These make it real.
- **The transferable lessons** — what a reader could take away and apply.
- **The concrete proof** — real numbers, the live result, what actually works.

If the artifacts don't contain a real decision or lesson, don't manufacture one — a shorter honest story beats an inflated one.

## Step 2: Find the hook

Draft 2-3 opening lines that lead with tension or a recognizable moment, and pick the strongest with the user. The hook is the single most important sentence — if it doesn't make someone want line two, nothing else matters. Test: would a stranger scrolling stop on this?

## Step 3: Draft the story

A structure that works for the build-story genre (adapt to the actual project):

- **The hook** — the problem/tension, felt, in the first two lines.
- **Why it mattered** — who has this problem, why it's worth solving, why the builder cared.
- **The key decisions** — 2-4 real forks, each: what I chose, what I gave up, why. This is where judgment shows. Do not list every step; pick the decisions a reader learns from.
- **The honest part** — a near-miss, a cut, a bug caught, something that changed. Builds trust.
- **What it does now** — the shipped result, concretely, with real proof/numbers. Brief.
- **The lesson(s)** — what the builder (and reader) takes away.
- **A light close** — what's next, or an invitation to try it. Never a hard sell.

Keep it tight. A build story is usually 400-800 words for a post, longer only if the project earns it.

## Step 4: Match length and channel

Ask the user where this is going and size accordingly:
- **LinkedIn post:** ~200-400 words, punchy, headers or line breaks, one clear takeaway.
- **Blog/long post:** 600-1200 words, room for the decisions and lessons in depth.
- **Portfolio page:** structured, scannable, with the outcome and the process both visible.

If the user wants more than one, write the long version first, then cut it down — cutting is easier than padding.

## Step 5: Check in and refine

Share the hook and structure before writing the full thing; the hook especially needs the user's sign-off. After drafting, the user reviews for accuracy (it's their story and their voice) — fix anything that isn't true to what happened or how they'd say it.

## Anti-patterns

- Never open with "X is a tool that…". Lead with tension the reader feels.
- Never write a step-by-step project log. Pick the decisions and lessons; skip the rest.
- Never invent decisions, numbers, struggles, or lessons. Pull the real ones from the artifacts.
- Never say "hire me," "I'm skilled at," or otherwise claim the capability — show it, let the reader conclude it.
- Never bury the honest/messy part — it's what makes the story credible.
- Never let it get long and dense. Skimmable, one idea per paragraph.
- Never write in a voice that isn't the builder's — the user reviews for voice.

## Rules

- Grounded in the real artifacts; nothing invented.
- Lead with tension, teach a lesson, let capability be implicit.
- The hook earns its place first — get it right before the rest.
- Honest about the messy middle; that's the credibility.
- Skimmable, tight, phone-readable.
- The user owns the final voice and accuracy.

## Exit checklist

- [ ] Artifacts read; the real problem, decisions, near-misses, and lessons pulled
- [ ] A hook that leads with tension and would stop a scroll, signed off by the user
- [ ] 2-4 real decisions told with what-was-given-up, not a full step log
- [ ] At least one honest/messy moment included
- [ ] Concrete proof (real result/numbers) present but brief
- [ ] One clear transferable lesson
- [ ] Sized to the channel; light close, no hard sell
- [ ] User reviewed for accuracy and voice

## Handoff

This is the final pipeline stage. When the story is written and the user approves it, the pipeline is complete for this product — the idea has gone from problem to shipped MVP to public story. If the user wants versions for multiple channels (LinkedIn, blog, portfolio), produce them from the approved long version. Point out that the case study, the product, and the pipeline artifacts together form a portfolio-ready package.