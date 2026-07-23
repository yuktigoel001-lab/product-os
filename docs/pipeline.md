This is the spine of the Product OS. Every product idea travels through the same ordered sequence of stages, from a rough thought to a shipped, documented MVP. Each stage has one job, is run by one skill, and produces one output that becomes the next stage's input.

The point of a fixed pipeline is to remove "what do I do next?" from every project. The order is deliberate: you cannot write a PRD before an idea is validated, and you cannot build before the work is scoped. This chaining is what prevents the most common failure mode — jumping straight to building something that shouldn't be built.

## How to use it

- **Follow the stages in order.** A stage's output is the next stage's input.
- **I review and approve every output before the next stage begins.** No stage proceeds until I've signed off on the previous one. This is mandatory, especially in the early phase.
- **My feedback improves the skill- but only the reusable parts.** When my review reveals a _reusable_ lesson ("PRDs should always state what's out of scope"), that lesson is folded back into the skill so future runs start better. When my feedback is a _project fact_ ("this PRD should mention Spotify"), it stays in the project doc and never touches the skill. Never mix project-specific content into a skill — that is how skills rot into generic mush.
- **Skipping is allowed, but only with permission.** Not every project needs every stage (see stage 3). Never skip a stage silently — ask first.
- **Each output is a file**, written as a filled-in instance of a template from `templates/`. The files live in each project's own `docs/` folder.
- **Build skills just-in-time.** A skill is built the first time a project reaches its stage — not all upfront.
- **Every new or edited skill passes through `skill-validator` before it enters the system.** No skill is added to `skills/` until skill-validator has reviewed it and I've approved that review. (See "The skill-validator gate" below.)

## How the pipeline is invoked

The pipeline is run manually, by me, in plain English. The manual effort is deliberate, because I review every output, and automation would run stages without me. The "trigger" is me describing an idea in plain English and confirming. The "engine" is this file plus `CLAUDE.md`, which together tell Claude how to behave at each stage.

### Starting a new idea

I describe the idea in my own words. For example:

> "I have this problem I want to solve as a product manager and build a prototype for."

> "I want to turn this idea into an MVP I can show my leadership."

When Claude recognises that I'm bringing a new product idea, it **asks for confirmation before starting anything**:

> "Would you like to take this idea through the Product OS pipeline and turn it into an MVP?"

Only after I confirm does the pipeline begin, starting at stage 1 (`problem-definer`). Claude never assumes an offhand mention of an idea is a decision to build it — the confirmation is the gate between thinking out loud and starting work.

### Moving through the stages

Once the pipeline is running, each stage works the same way:

1. Claude runs the current stage's skill and produces its output file.
2. Claude **stops and waits for my review** — it does not move on.
3. I approve, or give feedback. Reusable lessons fold into the skill; project facts stay in the project's doc.
4. Only after my approval does the pipeline advance to the next stage. Claude tells me which stage is next and what it will produce, then waits again.

I never have to name the next skill. Claude knows the order from this file.

### Resuming later

Returning to a project mid-pipeline, I say something like **"where are we"** and Claude reads `docs/` in pipeline order, tells me the current stage, and names the single next action.

## The skill-validator gate

Skills are just markdown instructions, and skills cloned from other repos can contain unsafe or corrupting instructions (prompt injection, attempts to override CLAUDE.md, actions a skill has no business taking). `skill-validator` is the gate that protects the whole system: before any new or edited skill is added, it checks for —

- **Hygiene / injection:** does the skill try to override my rules, exfiltrate anything, ignore CLAUDE.md, or take actions outside its stated job?
- **Structural fit:** does it match the skill format, have one clear job, and fit an actual pipeline stage?
- **Scope discipline:** does it stay a reusable _process_, or has project-specific content leaked in?

`skill-validator` is a smoke detector, not a force field — it catches obvious problems but does not make an unreadable skill safe. I still read what I clone. Because it guards every other skill, it is the **first skill built**, before any pipeline-stage skill.

## The pipeline

| #   | Stage                 | Skill                          | Input → Output                             | The question it answers                                                                                                       |
| --- | --------------------- | ------------------------------ | ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| 1   | Define the problem    | `problem-definer`              | Rough idea → `problem.md`                  | Who exactly has this, how often, how painful, and what do they do about it today?                                             |
| 2   | Validate              | `idea-validator`               | `problem.md` → `validation.md`             | Is this worth building? (GO / ITERATE / STOP)                                                                                 |
| 3   | Build decision rules  | `rubric-builder`               | A fuzzy judgment call → `[name]-rubric.md` | How do I turn "I'll know it when I see it" into a rule that can be applied consistently?                                      |
| —   | Dry run (manual)      | _(none — deliberately manual)_ | Rubric → `dry-run-log.md`                  | Does the rubric actually produce the right call on real examples?                                                             |
| 4   | Write the PRD         | `prd-writer`                   | `validation.md` + my answers → `PRD.md`    | What is v1, what's out, who is it for, and what does "done" mean?                                                             |
| —   | PRD review panel      | _(sub-agents, not a skill)_    | `PRD.md` → panel feedback                  | What would an engineer, designer, skeptic, customer — and where relevant a domain expert — object to before this is approved? |
| 5   | Scope the build       | `prototype-scoper`             | `PRD.md` → `build-plan.md`                 | Skill or app? What is the ~1-week cut, and what gets left out?                                                                |
| 6   | Design spec           | `design-spec`                  | `build-plan.md` → `design.md`              | What exactly does Claude Code build — structure, screens/output shape, data?                                                  |
| 7   | Build                 | `vibe-coding`                  | `design.md` → working MVP in `src/`        | Build it, with guardrails for a non-technical builder.                                                                        |
| 8   | Ship & tell the story | `case-study-writer`            | Shipped MVP → `README.md`                  | How do I present this as portfolio evidence?                                                                                  |

## Notes on specific stages

**Stage 3 (rubric-builder) is conditional.** It only runs when a project has a core judgment call at its heart — for example, "is this piece of content relevant to the learner's goal?" Some projects don't have one and skip it.

**The dry run between stages 3 and 4 is intentionally manual.** Before trusting a rubric, it is hand-tested against 8–10 real examples and logged. If the rubric disagrees with your own judgment, the rubric is wrong — fix it here, on paper, where it is cheap.

**Product vision and trade-offs are not separate stages.** They live as sections inside the PRD (stage 4). For a one-week MVP, vision is a paragraph and trade-offs are a "what we are NOT doing and why" section — not standalone processes.

**Stage 4 ends with a review panel, not with my approval.** Once `prd-writer` produces the PRD, it is pressure-tested by sub-agents before I sign off: **AI Engineer, AI Product Designer, Skeptic, and Customer** always, plus a **dynamic SME** when the problem sits in a specialized industry (fintech, healthcare, legal, etc.). Each reviews through its own lens only. I read the panel's concerns, decide what to act on, and only then approve the PRD. The panel roles are defined in `CLAUDE.md`.

**The SME agent is only used with research behind it.** An AI told to "act as a domain expert" will invent domain facts confidently. So when a specialized- industry project needs an SME, the `industry-research` or `workflow-research` skill runs first and its output grounds the review. SME and research are always coupled — never one without the other. Both are built just-in-time, the first time a project actually needs them.

**Panel agents are built just-in-time too.** Don't build all five upfront. Build each one the first time a project's PRD actually needs that lens.

**Positioning is not a separate stage either.** It is the opening of the case study (stage 8).

**`skill-validator` is a system gate, not a pipeline stage.** It does not appear in the table because it does not run on a project — it runs on _skills_, every time one is added or edited. Think of it as the doorway into `skills/`, not a step on the project's path.

## This pipeline is a draft that improves through use

The first committed version of this file is not final, and that is by design. When a real project travels through the pipeline, some stage will turn out to be mislabelled, or two stages will want to merge. When that happens, this file gets updated. A pipeline that shows a few commits of refinement-through-use is stronger evidence of real product thinking than one that was born perfect.