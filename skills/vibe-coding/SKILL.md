---
name: vibe-coding
description: "Builds the actual app for a non-technical PM, as a controlled, screen-by-screen process — not a black-box code dump. Use this as the build stage of the Product OS pipeline, after design.md exists, when it's time to turn the PRD's build prompt + the design spec into a working app. Trigger on 'build it', 'start the build', 'let's make the app', or any point where the spec and design are locked and the app is ready to be built. This skill builds to the approved spec and design; it does not decide scope (that's the PRD) or design (that's design-spec). It builds one screen at a time, verifies each with the user before moving on, and treats graceful failure, key safety, and the caching fallback as mandatory gates that cannot be skipped."
---

# Vibe Coding

The build stage. Turns the PRD's build prompt + `design.md` into a working app — built *with* a non-technical PM, not *at* them. The person can't read code fluently, so the build must be legible: explained in plain English, shown screen by screen, verified at each step, and never allowed to skip the safety requirements that keep a live demo from breaking.

Read the PRD/build prompt, `design.md`, and any rubric or data spec before starting. Build exactly to them. If something in the spec is ambiguous or missing, ask — don't invent scope.

## The two rules that govern the whole build

1. **Explain before you build, in plain English.** Before writing any code for a screen or a piece of logic, say what you're about to do and why, in words a non-technical PM understands. Wait for their go-ahead. Never dump a wall of code without the plain-English version first.

2. **Build screen by screen, verify each before the next.** Build one screen (or one self-contained piece), show it working, let the user confirm it looks and behaves right, THEN move on. Never build the whole app in one pass — the user must be able to follow along and catch problems while they're small.

## Gates — the safety net for THIS build

A "gate" is a build requirement that must pass before the build is done. Different products need different gates — a data app, a payments flow, an offline app, and a live-API app each fail in different ways. So this skill does NOT impose one fixed checklist. It combines a few universal gates with a set derived from *this* product's architecture.

### Step A — The universal gates (apply to almost any app)

1. **Secret safety** — if the app uses any keys, tokens, or secrets: read them from a local settings file (e.g. `.env`), NEVER in the code, NEVER committed; confirm `.env` is gitignored; walk the user through creating each secret themselves (never handle the value); set a hard spending cap on any PAID service. If the app has no secrets, state that and move on.
2. **Handles the unhappy path** — every app has failure modes (bad input, a failed call, an empty state, no results). Whatever they are for this app, they must be handled cleanly — a clear, intentional-looking state, never a raw error or a crash. Identify this app's actual failure modes and handle them.
3. **Applies the design spec** — if there's a UI and a `design.md`: build to its exact palette, type, spacing, and components, not defaults; give the emotional-center screen its polish. If there's no UI, skip.

### Step B — Derive THIS product's specific gates (do this before building)

Read the PRD/build prompt and the design spec, and ask: **what does this app's architecture actually require to be safe and reliable?** Derive the project-specific gates from that — don't guess, and don't impose gates from other products. Then confirm the list with the user before building.

Prompts to surface them (not an exhaustive list — reason from the actual product):
- Does it make live/external calls? → likely gates: graceful degradation on failure, and a cached/reliable path for any demo that depends on those calls.
- Does it handle money or transactions? → likely gates: transaction integrity, idempotency, confirmation before irreversible actions.
- Does it work offline or sync data? → likely gates: sync/conflict handling, offline states.
- Does it take user-generated or external data? → likely gates: input validation, handling malformed/empty data.
- Does it store personal or sensitive data? → likely gates: safe storage, not logging secrets.
- Is there a single "this must never break in front of a reviewer/user" moment? → likely gate: a guaranteed-reliable path for that moment.

State the derived gates plainly, e.g.: "For this app, on top of the universal gates, the gates are: [X, Y]. Here's why each." Get the user's confirmation, then build to them.

### The rule
The build is not done until every applicable universal gate AND every derived gate passes. State each gate's status honestly at the end. A gate that doesn't apply is marked not-applicable, not silently dropped.

## Build sequence

1. **Set up the skeleton + secrets first.** Project structure, the local settings file, `.gitignore`, and the design tokens from the design spec as the base styling. Confirm any secrets load safely (Gate 1) before building features.
2. **Build the core logic before the screens, but verify it in plain terms.** Whatever the app's central engine is (from the build prompt), build it first, then show the user it produces a real result — and if it depends on live calls, cache the demo result (a derived gate — see Step B). Explain what it did in plain English.
3. **Then build the screens one at a time**, in flow order, each verified before the next:
   - Each screen: explain → build → show it working → user confirms → commit → next.
   - Apply design.md on every screen (Gate 3).
   - Wire each screen to real data from the engine as you go.
4. **Test the failure paths on purpose** (Gate 2) and show they degrade cleanly.
5. **Full walkthrough** — run the whole thing end to end on the cached path, confirm it matches the PRD's "done" (the 60-second walkthrough that never breaks).
6. **Commit at each verified step**, plain-English messages. Keep the working tree clean.

## Working with a non-technical builder

- Plain English always. Explain any technical term the moment it's used.
- When a decision needs the user, give the choice in everyday words with a recommendation — don't make them research it.
- If something breaks or is harder than expected, say so plainly and give options, not jargon.
- Commit often so there's always a working point to return to.
- Never let the build outrun the user's understanding. If they're lost, slow down and re-explain before continuing.

## Anti-patterns

- Never dump the whole app at once. Screen by screen, verified.
- Never write code without the plain-English explanation first.
- Never skip a mandatory gate to move faster. An unmet gate = an incomplete build, stated honestly.
- Never hardcode or commit a secret. Ever.
- Never let a live call fail into a raw error or broken screen — degrade cleanly (when the app has live calls).
- Never ship a live-dependent demo without the cached fallback proven demo-safe.
- Never use default styling when a design spec specifies otherwise.
- Never invent scope not in the PRD. If it's not specified, ask.

## Rules

- Explain before building; build screen by screen; verify each step.
- Gates are mandatory, not optional: the universal ones plus the ones derived from this product's architecture. Derive them from the PRD; don't impose a fixed checklist.
- Build exactly to the PRD + design.md — no more, no less.
- Keep the person in the loop and never outrun their understanding.
- Commit at every verified step so there's always a safe point to return to.

## Exit checklist

- [ ] Universal gates handled: secret safety, unhappy-path handling, design spec applied (or each marked not-applicable)
- [ ] This product's specific gates were DERIVED from the PRD, confirmed with the user, and each passes
- [ ] Every applicable gate's status stated honestly; none silently dropped
- [ ] A failure path was tested on purpose where the app has failure modes
- [ ] Built screen by screen, each verified with the user before the next
- [ ] Full end-to-end walkthrough matches the PRD's "done" and never breaks
- [ ] Working tree clean, committed at each step with plain-English messages

## Handoff

When the app is built, verified end to end, and all applicable gates pass (universal + derived), the next and final stage is **case-study-writer (stage 7)** — it turns the shipped app into the portfolio case study. Tell the user that's next. If the plan includes deploying (e.g. Vercel/Railway) after local works, note that deployment happens before or alongside the case study, per the PRD.