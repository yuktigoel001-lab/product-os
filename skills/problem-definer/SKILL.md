---
name: problem-definer
description: "Turns a rough product idea or feature request into a sharp, written problem statement before any solution work begins. Use this any time someone is scoping a new idea, proposing a new feature, or jumping straight to a solution or technology ('let's add AI for this', 'we should build X') without a validated problem behind it. Trigger it even if the user opens with a feature name, a tech choice, or 'I want to build' — the job is to pull the real problem out from underneath. This is stage 1 of the product strategy pipeline: it defines the problem from a PM's lens only. It does not judge whether the idea is worth pursuing (that's the next stage) and does not design a solution."
---

# Problem Definer

Every idea and every feature request is a bet that some problem is real, specific, and worth solving. Most bets fail not because the solution was bad, but because nobody wrote down the problem first — so there was nothing to check the solution against. This skill's only job is to produce that check: a short, concrete problem statement, written down in `problem.md`, before any solutioning starts.

If the user starts describing what they'll build, that's fine — it's useful signal about what they're anchored on — but redirect gently: "Let's park that for a second and make sure we've got the underlying problem nailed down first. We'll come back to it."

## Step 0: Separate the itch from the tool

Before anything else, figure out whether you're looking at a problem or a solution wearing a problem's clothes. If the user opens with a feature, a technology, or "I want to build X," say so plainly and name it as the anchor it is — then set it aside for now. Don't write anything to `problem.md` until Steps 1–3 below are actually answered. Never fill in an answer on the user's behalf — if they don't know something, mark it `[NEED: ...]` and move on.

## Step 1: Ask four questions, in plain language

Your job here is to genuinely understand the problem the user wants to solve, and help them state it precisely enough that the next stage can validate it. Ask these conversationally, in your own words — never as a multiple-choice menu. Work with the user as a thinking partner, not a skeptic. When an answer is still fuzzy or a detail is missing, ask a gentle follow-up to help them get specific — not to make them justify the problem, but because a concrete `problem.md` field can't be written without it.

**1. Problem** — What's actually broken or painful right now, described as a symptom, not a fix? If the answer is really a feature description ("we need a dashboard"), ask: "If that feature didn't exist, what would still be going wrong for someone?" Also check: is this idea already anchored on a specific solution or technology? If so, name it out loud and set it aside — that's not the problem, that's the reflex.

**2. User** — Who, specifically, feels this? A job title, a segment, a situation — not "users" or "clients" or "everyone." If the answer is broad, help them zero in on the first real person who'd feel this most acutely, and picture the actual moment it happens to them: what were they doing right before it hit? A quick follow-up like "who's the one person this hits hardest?" usually gets there.

**3. Impact** — How often does this happen, and what does it cost when it does — time, money, churn risk, a worse client outcome, team burnout? And what do they do about it today? A workaround already in use is one of the best signals that a problem is real, so don't skip this — it also tells you what the bar for "better" actually is.

**4. Urgency** — Why does this matter now, as opposed to a quarter ago or a quarter from now? Has something changed — new client volume, a competitor, a deadline, a complaint pattern — or has this been quietly true for a while and just never got picked up? If nothing changed, that's worth naming too; it doesn't kill the problem, but it changes how urgently it should be prioritized.

**5. Build intent** — What is the user actually trying to achieve by building this? A portfolio piece to get hired, an internal tool for their team, a product to sell, a personal utility? This isn't part of the problem itself, but it's the lens every later stage calibrates against — "worth building" means something different for a portfolio demo than for a commercial product. Ask it plainly and capture their answer in their own words.

Move to Step 2 once all five have specific answers, or an explicit `[NEED: ...]` where the user genuinely doesn't know yet.

## Step 2: Restate it as one sentence, then gut-check it

Pull the four answers into a single restatement:

> [User] struggles with [problem] because [root cause], which costs them [impact] — and it matters now because [urgency].

Then run it past three quick checks. These aren't a formal framework — just the three ways problem statements most often go wrong. Name any that apply and fix the restatement before writing it down.

- **Is a solution hiding inside it?** If the sentence names a feature or a tool instead of a pain, strip it out. ("Struggles without a dashboard" → what are they actually failing to see or do?)
- **Is the user still a crowd?** "Businesses," "clients," "teams" aren't specific enough. If you can't picture one real person hitting this, ask one more gentle follow-up to bring it into focus.
- **Is this actually your problem, not theirs?** Sometimes what's driving the request is an internal metric or a business want, not something the user themselves is struggling with. Both are valid reasons to build something — but say which one this is, plainly, so nobody mistakes one for the other later.

## Step 3: Write problem.md

Fill in every field concretely, or with `[NEED: ...]` — never a guess dressed up as an answer.

```markdown
# Problem — [short name]

## One-line problem
[User] struggles with [problem] because [root cause], which costs them [impact] — and it matters now because [urgency].

## Problem
[The pain itself, as a symptom. No feature or technology named.]

## User
[The specific person or segment who feels this. Title, situation, context — not "everyone."]

## Impact
- **How often:** [daily / weekly / monthly / rarely]
- **What it costs:** [time, money, risk, churn, worse outcome — be concrete]
- **Current workaround:** [what they do about it today, and why it falls short]

## Urgency
[Why this matters now specifically. What changed, or why has it been overlooked until now.]

## Build intent
[What the user is trying to achieve by building this — portfolio piece, internal tool, product to sell, personal utility. The lens later stages calibrate against.]

## Anchored solution (set aside for now)
[Any feature/technology the user was already reaching for, noted so it isn't lost — but kept out of the problem statement itself. Write "none" if there wasn't one.]

## Problem type
[Whose problem this really is — the user's pain, an internal/business need, or both — and which one is driving the request.]

## Open questions for validation
[2–3 things the next stage should probe — usually the weakest of: how real the impact actually is, whether this is common enough to matter, or how it differs from the current workaround.]
```

## Anti-patterns

- Don't settle for "everyone," "clients," or "users" as the User — gently help the user name one real person every time. The aim is a usable answer, not a challenge.
- Don't offer multiple-choice options. Ask open questions in plain language and let the user articulate their own answer.
- Don't let a feature or technology sneak into the Problem or One-line fields — note it in "Anchored solution" instead.
- Don't fill in a field with a plausible-sounding guess. Use `[NEED: ...]` and move on.
- Don't rate or endorse the idea here. That's the next stage's job — this one only sharpens the problem.
- Don't skip the "what do they do today" question. A problem with no workaround on record is usually a problem nobody's actually tried to solve — which itself is worth flagging, not assuming.

## Worked example

**Good:** Account managers juggling 8+ client accounts lose track of which clients haven't been touched in a while, and only notice when a client raises it themselves — by which point some trust is already gone. Specific user (account managers, 8+ accounts), a real moment (a client raises it first), a concrete cost (trust, and the scramble to catch up), no feature named.

**Bad:** We need a client health dashboard so nothing falls through the cracks. This names the feature ("dashboard") before establishing what's actually falling through the cracks, for whom, or how often — there's nothing here to validate.

## Exit checklist

Before considering this done:

- [ ] Problem, User, Impact, Urgency, and Build intent all have real answers or `[NEED: ...]`
- [ ] The user is one specific person/segment, not a crowd
- [ ] No feature or technology is named inside the Problem or One-line fields
- [ ] The current workaround is recorded, not skipped
- [ ] Problem type (whose problem this really is) is stated plainly
- [ ] `problem.md` has no unfilled `[...]` placeholders left unintentionally

## Handoff

When `problem.md` is complete and the user approves it, the next stage is **idea-validator (stage 2)** — it takes this file and decides GO / ITERATE / STOP. Tell the user that's next and wait for them to start it. Do not run it automatically.