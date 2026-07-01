---
name: precost
description: |
  Runs a fast, visual "cost & value" pre-check on a Copilot Cowork task BEFORE
  the work starts. Reads five cheap, local cost signals — the model in use, the
  size of the context, the likely runtime, the tools / skills / plugins the task
  will need, and the weight of any attachments (an .md costs far less than a .pdf,
  image, or .pptx). Classifies the task as Light / Medium / Heavy, estimates the
  Copilot Credits and dollar cost, estimates the time saved and business value,
  shows it inline as a compact card with a short disclaimer, surfaces
  sustainability recommendations when the task could run leaner, then asks whether
  to proceed in Cowork, proceed in Cowork more sustainably, or use a lighter tool
  (Copilot Chat / M365 Copilot) instead.
  Invoke it when the user types "/precost", "precost", "precost check",
  "pre-check first", "cost check", "estimate this task", "what will this cost",
  "is this worth running in Cowork", or "should I run this here" — and at the start
  of every NEW task the user delegates to Cowork.
  Do NOT use for follow-up questions or refinements WITHIN a task already in
  progress — it runs once per new task, not on every message. Do NOT use to report
  the real metered cost of a finished task (that is the built-in /cost command and
  the Cost Management dashboard, not this estimate).
cowork:
  category: analysis
  icon: Calculator
---

# Pre-cost — Cowork Task Cost & ROI Pre-check

A lightweight gate that runs **once at the start of a new task** (or whenever the
user types **`/precost`**). Before any credits are spent, it tells the user
roughly what the task will **cost** and what it will **return**, shows it inline,
points out how to run it more **sustainably**, and lets them decide whether to
proceed, proceed leaner, or switch to a cheaper tool.

> **Pre-cost is an unofficial, user-created incubation skill. Every figure it
> produces is an estimate, not a bill or a spending limit.** The authoritative
> numbers are the built-in `/cost` command and the Cost Management dashboard,
> which run *after* a task completes.

Keep it **fast**. This is a quick estimate, not research. The only lookups
allowed are cheap, local ones: read the active model from the session, list
attachments, and read the companion reference files in this folder. Do **not**
call search, email, calendar, web, or file-content tools to produce the estimate.

## Companion reference files (load on demand — cheap local reads)

The pricing and value detail lives in three files in this folder so this workflow
stays short. **Read the relevant file when a step says to.**

- **`pricing-reference.md`** — model cost multipliers, attachment weights, base
  credit bands, and the adjustment formula. Use it in Steps 1–3.
- **`value-and-routing.md`** — time-saved / value bands and formula, verdict
  logic, which-Copilot-to-use routing, and step-by-step instructions for doing
  the task in M365 Copilot / Copilot Chat. Use it in Steps 4, 6, and 8.
- **`card-template.md`** — the ready-to-fill visual card skeleton. Use it in
  Step 7.

These files are the **single source of truth** for every number this skill
quotes. Do not invent figures that aren't in them.

## When to run

- The user types **`/precost`** (or "precost", "pre-check first", "cost check").
- The user has just delegated a **new task** to Cowork — the first substantive
  request of a task (e.g. "prep me for my customer meeting and build a deck",
  "analyze this data and produce a report", "draft and send the team update").

## When NOT to run

- **Follow-ups within the same task** — "make the title bigger", "add a slide",
  "now email it too". The pre-check already ran; don't run it again.
- Pure questions / chit-chat that aren't a delegated task.
- A request for the **actual** cost of a completed task — point the user to the
  built-in `/cost` command and the Cost Management dashboard instead.

## Step 1 — Gather the five cost signals (cheap, local only)

Read these five signals from the prompt + session + a quick attachment listing:

1. **Model in use.** Detect the active model and apply its credit multiplier
   (`pricing-reference.md` §4, anchored to the Cowork default Opus 4.8 = 1.0×;
   1 credit ≈ $0.01). If it can't be determined, assume Opus 4.8 (1.0×) and say so.
2. **Context size.** Roughly how much material the model must read/hold. Judge it
   **small / moderate / large**.
3. **Runtime.** Light ≈ under a minute; Medium ≈ 1–3 min; Heavy ≈ 3 min+.
4. **Tools / skills / plugins.** Cheap (a single read), moderate (multi-source
   search, a doc skill, a few tool calls), or expensive (image generation, deep
   research, browser automation, subagents).
5. **Attachments.** List them and note type + size. **Format drives credit weight
   far more than file size** (`pricing-reference.md` §5; `.md` cheapest).

> Read `pricing-reference.md` now for the model-multiplier and attachment-weight
> tables.

## Step 2 — Classify the base task (Light / Medium / Heavy)

Judge the task on sources, reasoning depth, and deliverables to set the **base**
credit band (`pricing-reference.md` §6). Pick the class by the **heaviest signal
present** — one short summary = Light; a multi-source briefing + Excel + deck =
Medium; a 6-month analysis + leadership report = Heavy.

## Step 3 — Adjust the estimate (model + one class bump)

Start from the base band, then adjust it with only **two** levers, using the
formula in `pricing-reference.md` §7:

```
effective_class  = base_class, bumped up one level for a heavy input / expensive tool
adjusted_credits ≈ base_band(effective_class) × model_multiplier
adjusted_cost_usd ≈ adjusted_credits × $0.01
```

1. **One-level class bump.** Move the base class **up one level** for a **heavy
   input** (`.pptx`, scanned/image PDFs, several images — the ≥ ~2× rows in §5)
   **or an expensive tool** (image generation, deep research, browser
   automation, subagents). Move it **down one level** only for a single trivial
   light read. Read the band from §6 for this *effective* class.
2. **Model multiplier.** Scale that band by the active model's multiplier,
   anchored to Opus 4.8 = 1.0× (Sonnet 0.6× eases it down; a 2.0× premium model
   pushes it up).

**Do not also multiply by attachment weight or a context/tool factor** — the
attachment weight only decides whether to trigger the class bump; multiplying by
it as well would double-count the same signal (the old formula's bug) and detach
the number from the badge.

Keep the result a **band**, never false-precise — e.g.
"≈ 200–450 credits · ≈ $2–4.50 (Sonnet 4.6)".

## Step 4 — Estimate the return (time saved + value)

Map the task to the Cowork ROI categories and **sum the typical minutes saved**
for the categories it touches (`value-and-routing.md` §1). Apply the value
formula with the default `HOURLY_RATE` (€75/hr; state it so it's transparent).
Cost is USD; value is the user's currency — don't invent an FX rate, present them
side by side.

## Step 5 — Sustainability check

Decide whether the **same outcome** could be reached for fewer credits. Only raise
levers that genuinely apply:

- **Model right-sizing** — routine task on a heavy model? Suggest Sonnet 4.6 / an
  efficiency model. Genuinely hard reasoning? Keep the heavy model.
- **Lighter attachments** — recommend converting a heavy PDF / image-heavy input
  to `.md` first.
- **Tighter scope** — narrow the timeframe, sources, or number of deliverables.
- **Cheaper route** — single artifact or quick Q&A? Point to Copilot Chat /
  M365 Copilot (see Step 6).

If at least one lever applies, prepare a **sustainable rewrite** of the prompt to
offer in Step 8. If nothing meaningful applies, say it already runs efficiently.

## Step 6 — Verdict & whether to suggest an alternative

Apply the verdict logic and routing table in `value-and-routing.md` §2–§3:

- **Strongly positive — proceed.** Time-value clearly dwarfs credit cost (typical
  for Medium/Heavy multi-deliverable tasks).
- **Marginal — offer a lighter tool.** A Light task a per-seat tool does at no
  metered credit cost. Suggest the alternative but let the user choose.

## Step 7 — Render the visual card (inline)

Render the estimate as a compact card **inline in the conversation** (never write
it to a file). Fill the skeleton in `card-template.md`. Include, in order:

1. **Title** — "Cowork task pre-check".
2. A **badge** for the class: Light / Medium / Heavy.
3. A **fact list**: Model, Estimated cost (adjusted band), Attachments,
   Estimated time saved, Estimated value (state the hourly rate), Verdict.
4. **Recommendations** (only if Step 5 found levers) — a short list.
5. A short, subtle **disclaimer** — use this exact wording:

   > *Estimate only — not the metered bill. It factors the model, context,
   > runtime, tools and attachments, but the real cost depends on what actually
   > runs and is shown by /cost and the Cost Management dashboard after the task.
   > This pre-check is advisory, not a spending limit, and uses research-based
   > pricing and time-savings bands (directional, not a guarantee). Running this
   > check itself uses a small amount of credits.*

## Step 8 — Ask how to proceed

Immediately after the card, ask one question so the user decides after reading the
numbers. Tailor the options to what applies:

- **"Proceed in Cowork"** — run the task as written (recommend for Medium/Heavy).
  Offer a **suggested optimized Cowork prompt** alongside this.
- **"Use Cowork — sustainably"** — *offer whenever Step 5 found a lever.* Apply
  the sustainable rewrite (switch the model where supported, convert heavy
  attachments to `.md`, tighten scope), briefly list the adjustments, then run.
- **"Use Copilot Chat / M365 Copilot instead"** — *offer for marginal/Light
  tasks.* Read `value-and-routing.md` §4, pick the matching recipe, and walk the
  user through the concrete steps for that tool. Provide a **suggested Copilot
  prompt**. Then stop — don't run it in Cowork.

If the user cancels, acknowledge and wait. Never block the task behind more than
these questions.

## Guardrails

- **Run once per task, at the start.** Never re-run on follow-ups.
- **Only cheap, local lookups for the estimate.** Detect the active model, list
  attachments, and read the companion files. No search/email/calendar/web/file
  tools.
- **Never present the estimate as the real bill.** Always show the disclaimer.
- **Quote ranges, not false precision.** Cost is a band read from the effective
  class and scaled only by the model multiplier (heavy inputs / expensive tools
  move the class up one level — they are not extra multipliers); value uses a
  stated, user-editable hourly rate.
- **Recommend sustainability only when it genuinely helps.** Don't invent levers.
- **Advisory, not enforcement.** Only admin spending limits cap spend.
- **Card is inline only** — never written to a file.
- **No fabrication.** Use only the bands, multipliers, weights, time-savings and
  routing in the companion files, plus the signals you can actually observe. If
  the task doesn't map cleanly, say it's a rough estimate rather than guessing.
