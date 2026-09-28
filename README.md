# Product OS

A reusable Claude Code setup that takes a product idea from a rough problem statement to a shipped, documented MVP — one stage at a time, with a human reviewing every step.

> **A note from the builder.** I'm an aspiring product manager. I don't have the title yet, so I built the system I wished I had — and let the building teach me the craft. This repo is that system. It's also the first thing I've ever version-controlled on GitHub. The commit history is part of the point: you can watch the thinking get sharper over time.

Clone it, point Claude Code at it, and describe your idea in plain English.

## Why this exists

Most product ideas die in the gap between "I have an idea" and "here's a working thing." Not because the idea was bad, but because there was no path between the two — no order of operations, no forcing function to define the problem before building, no record of the thinking along the way.

Product OS is that path. It runs an idea through the same stages every time, produces a written artifact at each stage, and won't move on until the previous step is signed off. Its main job, honestly, is to stop me from building things I haven't yet proven are worth building.

## How it works

Every idea travels through a fixed 7-stage pipeline, defined in [`docs/pipeline.md`](docs/pipeline.md):

1. **Define the problem** — turn a rough idea into a sharp problem statement (`problem-definer`)
2. **Validate** — decide whether it's worth building: GO / ITERATE / STOP (`idea-validator`)
3. **Build decision rules** — turn a fuzzy judgment call into a consistent rule, when a project needs one (`rubric-builder`, conditional)
4. **Write the PRD** — define what V1 is, what's out, what "done" means; ends in a ready-to-run build prompt (`prd-writer`)
5. **Design spec** — a real design pass: pull references, choose from 2–3 style directions, produce a `design.md` the build follows (`design-spec`)
6. **Build** — build the MVP screen by screen, in plain English, with safety gates (`vibe-coding`)
7. **Ship & tell the story** — turn the shipped product into a public build story (`case-study-writer`)

Each stage is run by one skill, produces one file, and stops for review before the next begins. You never name a skill or memorize a command — you describe your idea in plain English, and the pipeline takes it from there.

## The PRD review panel

Writing the PRD (stage 4) isn't a solo step. Before a PRD is approved, it's pressure-tested by a panel of sub-agents, each reviewing through one lens only:

- **AI Engineer** — is this actually buildable, and what's missing from the spec?
- **AI Product Designer** — is the flow clear, and where do users get confused?
- **Skeptic** — what could go wrong, and what untested assumptions is this resting on?
- **Customer** — would the real target user choose this over what they do today?

For problems in a specialized industry (fintech, healthcare, legal, and the like), a fifth reviewer joins: a **dynamic SME** spun up for that domain. Because an AI asked to "act as an expert" will invent domain facts confidently, the SME never reviews on assumed knowledge — its review is grounded in real research first. SME and research are always coupled.

The panel returns its concerns; the human reads them, decides what to act on, and only then approves the PRD.

## How it's structured

Two repos, kept deliberately separate — this separation is the design:

- **`product-os`** (this repo) — the reusable *machine*: the pipeline, the skills, the templates. It never holds one project's work.
- **A project repo** (e.g. a private `learning-os` I'm dogfooding on) — a real idea *travelling through* the machine, with its own `problem.md`, `validation.md`, and so on.

Inside this repo:

```
product-os/
├── CLAUDE.md        Governs how Claude Code behaves here
├── docs/
│   └── pipeline.md  The pipeline: stages, rules, how it's invoked
├── skills/          One skill per pipeline stage (built as needed)
└── templates/       Reusable output shapes the skills fill in
```

Three kinds of parts, kept strictly apart: **skills** are repeatable *processes*, **templates** are empty *shapes*, and **filled-in project docs** live in the project's own repo — never here. Keeping project specifics out of the shared skills is what stops them rotting into generic mush.

## What building this taught me

- **Cutting scope is a skill, not a failure.** I collapsed the pipeline from 8 stages to 6 to fight bloat — then split design back out into its own stage once I was honest that "a palette and two fonts" isn't a design direction.
- **A spec is only as good as its handoff.** Each stage's output is literally the next stage's input, so a vague PRD produces a vague build. The chaining forces clarity.
- **The messy middle is the real work.** I caught my own mistakes — including a change from a parallel session that quietly reverted a skill — by reviewing every step in the git history instead of trusting the first output.

## How to use it

1. Clone this repo and open it in Claude Code.
2. Create a separate repo for your actual project.
3. Describe your idea to Claude Code in plain English; confirm when it asks whether to run the pipeline.
4. Move through the stages one at a time, reviewing each output before moving on.

## Status

Early and evolving — by design. Skills are built just-in-time, the first time a project reaches a stage that needs one, so this repo grows as real projects travel through it. The pipeline is meant to be refined through use, not frozen.

## Credit

Built with Claude Code, directed by me. The pipeline draws on ideas from the PM community building with Claude, adapted into a personal system.

## License

© 2026 Yukti Goel. All rights reserved. This repository is proprietary — see [LICENSE](LICENSE). It's public so you can read it and see how it's built; it is **not** licensed for reuse, copying, modification, or redistribution without written permission.
