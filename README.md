# Product OS

A reusable Claude Code setup that takes a product idea from a rough problem statement to a shipped, documented MVP.

It's built for any PM with a specific goal — a problem to solve, a product to ship, a portfolio to build — who wants a structured way to get from idea to artifact instead of staring at a blank page. Clone it, point Claude Code at it, and describe your idea in plain English.

## Why this exists

Most product ideas die in the gap between "I have an idea" and "here's a working thing." Not because the idea was bad, but because there was no path from one to the other — no order of operations, no forcing function to define the problem before building, no record of the thinking along the way.

Product OS is that path. It's an opinionated pipeline that runs an idea through the same stages every time, produces a written artifact at each stage, and keeps a human in the loop reviewing every step.

## How it works

Every idea travels through a fixed pipeline, defined in [`docs/pipeline.md`](docs/pipeline.md):

1. **Define the problem** — turn a rough idea into a sharp problem statement
2. **Validate** — decide whether it's worth building (GO / ITERATE / STOP)
3. **Build decision rules** — turn fuzzy judgment calls into consistent rules (when a project needs it)
4. **Write the PRD** — define what v1 is, what's out, and what "done" means
5. **Scope the build** — cut it down to a ~1-week buildable plan
6. **Design spec** — specify exactly what gets built
7. **Build** — build the MVP with Claude Code
8. **Ship & tell the story** — write the case study

Each stage is run by one skill, produces one file, and stops for review before the next stage begins. You never name a skill or memorize a command — you describe your idea in plain English, and the pipeline takes it from there.

## The PRD review panel

Writing the PRD (stage 4) isn't a solo step. Before a PRD is approved, it's pressure-tested by a panel of sub-agents, each reviewing through one lens only:

- **AI Engineer** — is this actually buildable, and what's missing from the spec?
- **AI Product Designer** — is the flow clear, and where do users get confused?
- **Skeptic** — what could go wrong, and what untested assumptions is this resting on?
- **Customer** — would the real target user choose this over what they do today?

For problems in a specialized industry (fintech, healthcare, legal, and the like), a fifth reviewer joins: a **dynamic SME** — a subject-matter expert spun up for that specific domain. Because an AI asked to "act as an expert" will invent domain facts confidently, the SME never reviews on assumed knowledge alone — its review is grounded in real research first (via a research skill built for that project). SME and research are always coupled.

The panel returns its concerns; the human reads them, decides what to act on, and only then approves the PRD. Like the skills, panel agents are built just-in-time — the first time a project's PRD actually needs that lens.

## What's in here

```
product-os/
├── CLAUDE.md        Governs how Claude Code behaves in this repo
├── docs/
│   └── pipeline.md  The pipeline: stages, rules, and how it's invoked
├── skills/          One skill per pipeline stage (built as needed)
└── templates/       Reusable output shapes the skills fill in
```

Three kinds of parts, kept strictly separate:

- **Skills** are repeatable *processes* — one per stage.
- **Templates** are empty *shapes* of outputs, with blanks to fill.
- **Project docs** are the *filled-in instances*, and they live in each project's own repo — not here.

## How to use it

1. Clone this repo and open it in Claude Code.
2. Create a separate repo for your actual project (Product OS builds the tool; your project repo holds the work).
3. Describe your idea to Claude Code in plain English. Confirm when it asks whether to run the pipeline.
4. Move through the stages one at a time, reviewing each output before moving on.

## Status

Early and evolving. Skills are built just-in-time — the first time a project reaches a stage that needs one — so this repo grows as real projects travel through it. The pipeline itself is designed to be refined through use, not frozen.

## Credit

The pipeline and setup draw on ideas from the PM community building with Claude Code, adapted into a personal system.