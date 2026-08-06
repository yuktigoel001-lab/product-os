---
name: rubric-builder
description: "Turns a fuzzy, judgment-heavy decision at the heart of a product into an explicit rule that produces the same answer every time it's applied. Use this as stage 3 of the Product OS pipeline, after idea-validator returns GO, when the product's core value depends on a repeated 'is this X or not' / 'which bucket' / 'what order' judgment (e.g. 'is this content relevant to the goal', 'is this lead qualified', 'does this ticket need escalation'). Trigger on 'build a rubric', 'how do I decide consistently', 'turn this judgment into a rule', or any core classification/ranking the product must do again and again. This is a conditional stage — projects with no core judgment call skip it and go straight to prd-writer. This skill writes the rule; it does not write the PRD (stage 4) or build anything."
---

# Rubric Builder

Stage 3 of the pipeline, and only for projects whose core value *is* a repeated judgment call. If the product's magic is "it figures out which content matters," or "it decides which leads to chase," then that judgment can't be left to vibes — it has to be an explicit rule that gives the same answer every time, whether a person or an AI applies it. This skill produces that rule: `[name]-rubric.md` (e.g. `relevance-rubric.md`).

A rubric that only works when *you* apply it isn't a rubric — it's your intuition wearing a costume. The test of a good one is consistency: two people, or the AI on two different runs, reach the same verdict on the same item. Everything below is in service of that.

The rubric is **not trusted until it's dry-run tested** against real examples (the manual stage right after this one). This skill's job is to produce a rubric *and* set up that test — not to declare victory.

## Step 1: Pin down the judgment precisely

Before writing any criteria, get exact about what's being decided. Read `problem.md`, `validation.md`, and the CLAUDE.md scope to ground this in the real product.

- **The unit:** what single thing gets judged at a time? (One piece of content? One lead? One ticket?)
- **The possible outputs:** what are the allowed answers? Be specific:
  - Binary — in / out
  - Tiers — e.g. must-read / good-to-know / skip
  - An ordering — where does this sit in a sequence, and by what?
  - (Some products need two: a *classification* AND an *ordering*. Say so if that's the case.)
- **Who applies it, how often:** confirm this is a genuinely repeated judgment. A one-off decision doesn't need a rubric.

Don't proceed until the unit and the allowed outputs are unambiguous. If they're fuzzy, the rubric will be too.

## Step 2: Extract the criteria from the goal — not from thin air

The single most common failure is a rubric whose criteria are generic ("is it high quality?") instead of anchored to *this* product's goal. Pull the criteria from what actually matters here.

- From `problem.md` and the goal: what genuinely makes one item more valuable than another *for this specific user and goal*?
- List candidate criteria, then cut ruthlessly. For each, ask: **does this criterion actually change the verdict?** If two items differ on it but you'd judge them the same, it's not a real criterion — cut it.
- Aim for **3–6 criteria.** Fewer than 3 and you've probably restated the judgment; more than 6 and no one will apply it consistently.

## Step 3: Make each criterion concrete and checkable

A criterion is only useful if two people checking it against the same item get the same answer. Turn each one from a vibe into an observable test.

- Bad: "Is it relevant?" (that just restates the judgment)
- Bad: "Is it good quality?" (unobservable, subjective)
- Good: "Does it directly teach a skill named in the learner's goal, or a stated prerequisite of one?"
- Good: "Is it introductory, intermediate, or advanced relative to the learner's current level?"

Each criterion should be answerable using evidence *from the item itself* plus the goal — not outside knowledge the applier may not have.

## Step 4: Define the decision procedure

Criteria are useless without a rule for combining them into the output. Keep this as simple as works.

- **For binary/tiers:** what combination lands in each bucket? Use gates ("must directly teach a goal-skill, or it's out") or thresholds ("meets 3+ of the 4 criteria = must-read"). Prefer clear gates over fuzzy point-scoring.
- **For ordering:** what determines sequence? Name the ordering principle explicitly — prerequisite-before-dependent, foundational-before-advanced, current-level-first. If several apply, state their priority order.
- Write the procedure as steps someone could follow mechanically.

## Step 5: Handle the gray zone

Real items are borderline. A rubric that pretends everything is clear-cut fails on contact with reality.

- Name the most likely borderline cases for this judgment.
- Give an explicit default: "when genuinely unsure between X and Y, choose X because [reason tied to the goal]." A stated tie-breaker beats silent inconsistency.

## Step 6: Write [name]-rubric.md

Name the file for the judgment (e.g. `relevance-rubric.md`). Fill concretely, or `[NEED: ...]`.

```markdown
# Rubric — [what this judges]

## What gets judged
[The unit — one [item] at a time.]

## Possible outputs
[Binary / tiers / ordering — the exact allowed answers.]

## Grounding
[The goal and user this is anchored to, pulled from problem.md. One or two lines.]

## Criteria
| # | Criterion | The concrete test | What evidence answers it |
|---|-----------|-------------------|--------------------------|
| 1 | [name] | [observable test] | [what in the item shows it] |
| 2 | ... | ... | ... |

## Decision procedure
[Step-by-step: how the criteria combine into the output. Gates, thresholds, or ordering principle — mechanical enough to follow the same way twice.]

## Gray-zone defaults
[The likely borderline cases, and the explicit tie-breaker for each.]

## Known limits
[What this rubric deliberately does NOT handle, so its scope is honest.]
```

## Step 7: Set up the dry-run (mandatory, manual, next stage)

The rubric is a hypothesis until tested. Before it's trusted, it must be hand-applied to **8–10 real examples** and the results logged. Do NOT skip this — a rubric that's never been tested against real items is the single most common way this stage fails.

Set it up:
- Tell the user to gather 8–10 *real* examples from the actual domain (for learning-os: real pieces from their actual creators — a mix of clearly-relevant, clearly-irrelevant, and deliberately borderline).
- The user and the rubric each judge every item. Where they disagree, **the rubric is wrong, not the user** — that disagreement is the signal to fix a criterion or a default.
- Log it (the dry-run has its own file, `dry-run-log.md`). Iterate the rubric until it matches considered human judgment on the borderline cases.

Frame this to the user as: "The rubric's written — but we don't trust it yet. Next we test it on real examples and fix what breaks."

## Check in before writing

Before writing `[name]-rubric.md`, walk the user through the criteria and decision procedure conversationally and ask whether they match how the user *actually* judges these items. The user is the ground truth here — if a criterion doesn't match their real judgment, fix it before saving. Only write the file once they confirm.

## Anti-patterns

- Never write a criterion that just restates the judgment ("is it relevant?"). Break it into observable tests.
- Never include a criterion that doesn't change the verdict — cut it.
- Never leave the decision procedure implicit. Criteria without a combining rule aren't a rubric.
- Never declare the rubric done without the dry-run. Untested = unproven.
- Never resolve a dry-run disagreement by "correcting" the human to match the rubric. The human is ground truth; fix the rubric.
- Never let criteria depend on outside knowledge the applier won't have — anchor them in the item + the goal.
- Never exceed ~6 criteria. Consistency dies with complexity.

## Rules

- The measure of a rubric is consistency: same item, same verdict, every applier, every run.
- Anchor every criterion to *this* product's goal, pulled from problem.md — not generic quality.
- Prefer clear gates over fuzzy point-scoring.
- State gray-zone defaults explicitly; silent ambiguity is where consistency dies.
- The rubric is a hypothesis until the dry-run confirms it. Set up the test; don't skip it.

## Exit checklist

- [ ] The unit and allowed outputs are unambiguous
- [ ] 3–6 criteria, each a concrete observable test, each one that changes the verdict
- [ ] A mechanical decision procedure that combines them
- [ ] Explicit gray-zone defaults
- [ ] Known limits stated
- [ ] `[name]-rubric.md` written with no unfilled `[...]`
- [ ] The dry-run is set up and the user knows it's the required next step

## Handoff

When `[name]-rubric.md` is written and the user approves it, the next step is the **manual dry-run** (not a skill — deliberately hand-done): apply the rubric to 8–10 real examples, log results in `dry-run-log.md`, and iterate the rubric until it matches considered human judgment. Only after the dry-run holds does the project move to **prd-writer (stage 4)**.

Tell the user the dry-run is next and wait for them to run it. Do not skip ahead to the PRD on an untested rubric.