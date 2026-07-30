# PRD — [Product / feature name]

> `[NEED: my review]` — this template is a first version, committed for use but
> not yet finalized. Edit it with my own feedback the first time a project reaches
> the PRD stage, before relying on it.

> Stage 4 output. Fill every field concretely, or mark `[NEED: ...]` for anything
> missing — never guess. This PRD builds on `problem.md` (stage 1) and
> `validation.md` (stage 2); reference them rather than repeating them.

---

## 1. Summary

**Hypothesis:** [In one sentence: we believe that building X for [user] will
solve [problem], and we'll know we're right if [signal].]

**Build intent:** [From problem.md — portfolio piece / internal tool / product to
sell. The bar this PRD is written against.]

**Verdict carried forward:** [From validation.md — GO, or ITERATE-with-changes and
what changed.]

## 2. The problem (in brief)

[2–3 sentences, pulled from problem.md. Who struggles with what, and why it
matters. Don't re-derive it — this is a pointer, not a re-do. Link: `problem.md`.]

## 3. Who it's for

**Primary user:** [The one specific person/segment from problem.md.]

**Their goal:** [What they're trying to get done that this helps with.]

**Not for:** [Who this explicitly does not serve in v1. Keeps scope honest.]

## 4. What we're building (v1)

[The solution in plain English — what the user can actually do. Describe the
experience, not the tech. A few sentences or a short bulleted flow.]

**Core user flow:**
1. [Step]
2. [Step]
3. [Step]

## 5. Scope

**In scope for v1 (must have):**
- [The smallest set that proves the core value. If it's not essential to the
  hypothesis, it's not here.]

**Out of scope (the parking lot):**
- [Explicitly named things that are NOT in v1, and why. This section is as
  important as what's in — it's what stops scope creep.]

## 6. Key decisions & trade-offs

[The 2–4 real decisions made here, each with the trade-off. Format:
"Chose X over Y, because Z — accepting the cost of [what you gave up]."
This is where product judgment shows. Don't skip it.]

## 7. Success criteria

> Calibrate to the build intent. Don't force commercial metrics onto a portfolio
> or internal build.

**What "done" means for v1:** [The concrete finish line — the MVP works when a
user can [do the core thing] end to end.]

**How we'd know it's working** (choose what fits the intent):
- *Portfolio piece:* [demonstrates [what judgment], shows convincingly in a
  walkthrough, a reviewer understands it in under a minute]
- *Internal tool:* [team adopts it over the current workaround; [usage signal]]
- *Product to sell:* [metric with a baseline and a target, e.g. X% of [users] do
  [action], up from [baseline]]

## 8. Risks & open questions

| Risk / unknown | Why it matters | How we'd handle it |
|---|---|---|
| [risk] | [impact] | [mitigation, or `[NEED: ...]`] |

**Open questions for the next stage:** [Anything prototype-scoper or design-spec
needs to resolve.]

## 9. Simulation / data note (if a prototype)

[If v1 is a prototype on seeded data rather than a live build, state it plainly
here: what's simulated, what's real, and what a later version would connect.
Keeps the PRD honest about what's being proven.]

---

*Sources: `problem.md` (stage 1), `validation.md` (stage 2). Reviewed by the PRD
panel before approval — see CLAUDE.md for panel roles.*