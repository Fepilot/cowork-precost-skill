---
name: precost
description: |
  Community (not official Microsoft) pre-check that estimates what a Copilot
  Cowork task will cost before it runs. Reviews the prompt, asks up to 3 quick
  questions only if needed, then shows a visual card with credit band, ≈ USD,
  recommended model and effort, a leaner option with its minimum credits, the
  no-extra-credit Microsoft 365 Copilot route, time saved and a verdict, then
  asks how to proceed. Use when the user types "/precost", "precost", "/precost
  lite", "cost check", "estimate this task" or "is this worth running in
  Cowork". Do NOT use on follow-ups inside a running task or for the real cost
  of a finished task (that is /cost).
metadata:
  category: analysis
  icon: Calculator
---

# precost — Cowork cost & route pre-check

> **Community skill — not an official Microsoft skill.** Shared as-is to help
> people spend Copilot Credits wisely. Estimates are directional planning
> ranges, not quotes or bills. Copy it, adapt it and change the defaults in
> `pricing-reference.md` §0 to fit your organization.

**What it does:** prompt + `/precost` → (only if needed) up to 3 quick questions
→ one visual card (cost band, model, lean option, M365 Copilot route, verdict,
source link) → one "how do you want to proceed?" question → then the user's
choice runs. It never starts the actual task before the user decides.

**Keep the check itself cheap — it is metered too.** No web, mail, calendar,
file-content, people or SharePoint lookups, no subagents, no scripts. Allowed:
read the prompt and conversation, list attachments (names, types, sizes only),
Read the three companion files in this folder, ONE card, at most TWO question
prompts. Arithmetic comes from the lookup tables, not from tools.

## Companion files (cheap local Reads)

| File | Read it at | Holds |
|---|---|---|
| `pricing-reference.md` | Step 3 (always) | §0 your editable settings, official billing facts, task bands, model tiers, effort, tools, attachments, automations, lookup tables, source links |
| `card-template.md` | Step 5 (skip in lite mode) | the compact card JSON and fill rules |
| `value-and-routing.md` | Step 4 (§1–§3); Step 7 (§4 recipes) | time saved, verdict rules, routing, step-by-step M365 Copilot flows |

These files are the only source for numbers. Never invent a figure, model,
price, multiplier or feature that is not in them.

## Step 1 — Read the prompt (no lookups)

Take the task text written before/after `/precost` (or the user's previous
message). If there is no task text, ask one open question — "Paste the task you
want me to estimate" — and stop.

Extract the cost signals:
- **Outcome**: deliverables (type and count — doc, deck, sheet, email, app,
  image, dashboard) and quality bar (draft vs. exec-ready).
- **Actions**: send, schedule, post, update a system, browse a website.
- **Context**: sources (mail, chats, meetings, files, CRM / plugins, web) and
  time window.
- **Attachments**: list the workspace inputs (names, types, sizes only).
- **Recurrence**: one-off, scheduled (daily/weekly), or event-driven
  ("whenever an email arrives…").
- **Model & effort**: the current picker choice if the session shows it;
  otherwise "unknown — assumed Opus-class baseline".

## Step 2 — Clarify only if it changes the answer

Ask ONLY about unknowns that would move the class one level, change the route
(Cowork vs. M365 Copilot) or multiply the cost (recurrence). If the prompt
already answers them, skip this step entirely.

One AskUserQuestion call, max 3 questions, short options:
- **Outcome** — "What should the result be?" → one doc / email / summary ·
  several deliverables (doc + deck + sheet) · actions in apps (send, schedule,
  post, update records).
- **Scope** — "How much material should it use?" → a few items / last 7 days ·
  about a month of mail and files · many sources or months of data.
- **Frequency** — "Run once or repeat?" → one-off · weekly · daily or on every
  matching email/message.

An empty answer = cancel: acknowledge and stop.

## Step 3 — Estimate (Read `pricing-reference.md`)

1. **Class** — Light / Medium / Heavy from the official bands (§2), by the
   heaviest signal.
2. **Bump** — up one class for ONE heavy driver (§3: heavy input, expensive tool
   or plugin, many sources); down one for a single trivial read on a light input.
   Never stack bumps.
3. **Model tier** — map the model to Efficient / Baseline / Premium (§4) and read
   the band from the lookup table (§9). Unknown model → Baseline.
4. **Effort** — place the estimate inside the band (§5): Light → low end,
   Medium → middle, High / Extra High / Max → top end (Max on Heavy → flag
   "may exceed").
5. **Recurrence** — automations: per run AND per month (§8).
6. **Lean option** — same outcome with the levers in §10; its lower bound is the
   **lean minimum** (the least Cowork is likely to need).
7. **Share of monthly limit** — upper end of the chosen band vs. `MONTHLY_LIMIT`
   from §0 (state it is an assumption unless the user gave theirs).

Always quote ranges ("≈ 300–700 credits · ≈ $3–7"), never one exact number.

## Step 4 — Value, route & verdict (Read `value-and-routing.md` §1–§3)

- **Time saved**: sum the typical minutes of the ROI categories touched; value
  ≈ minutes × the per-minute rate in §1 (default €1.25/min = €75/h). Cost stays
  in USD and value in the user's currency; never invent an FX rate.
- **M365 Copilot route**: check the routing table (§3). If the outcome can be
  produced with Researcher, Analyst, the Word / Excel / PowerPoint agents,
  Copilot in the apps, scheduled prompts or Copilot Chat, name the shortest
  flow (tools in order). These run within the Copilot license (fair use) and do
  not meter Cowork credits — unless the user picks a frontier model there.
- **Verdict** (§2): ✅ Cowork as written · 🌱 Cowork, run it lean · 💡 Use
  M365 Copilot instead · ⚠️ Rescope first.

## Step 5 — Show the card (Read `card-template.md`)

Invoke the `render-ui` skill and make ONE `render_ui` call with the template,
filled in. Keep it compact: no extra sections, no restating the card in text.
The card always carries: the verdict, the class, the three KPI tiles (credits,
≈ USD, time saved), the comparison bar (as written · lean · M365 Copilot), the
recommended model + effort, the top cost drivers, the "run it lean" tips (only
if they apply), the source link, the community-skill note and the disclaimer.

**Lite mode** (`/precost lite`, "text only", or the user asked for minimal
credits): skip the card and `card-template.md`; reply with the 7-line text
summary described at the end of `card-template.md`.

## Step 6 — Ask how to proceed (one AskUserQuestion call)

Q1 "How do you want to run this?" — options (drop any that make no sense):
- **Proceed in Cowork** — "As written · recommended: <model> · effort
  <level> · ≈ <band>".
- **Cowork — sustainable** — "Lean plan: <2–3 levers> · ≈ <lean band> · needs
  at least ≈ <lean minimum> credits".
- **Use M365 Copilot instead** — "<tool flow, e.g. Researcher → PowerPoint
  agent> · no Cowork credits".
- **Rescope first** — only when the verdict is ⚠️.

Q2 (add only when the sustainable option is offered) "Credit budget for a
sustainable run?" → "Lean minimum ≈ <N>" · "Up to ≈ <lean band top>" · "No
budget — just run it lean".

## Step 7 — Act on the choice

- **Proceed in Cowork** — if the recommended model or effort differs from the
  current picker (or the picker is unknown), say in one line: "Set the picker to
  <model> · <effort> and send **go** — or send **go** now to keep your current
  model." Then stop and wait. On **go**, run the user's original task as
  written. This skill never selects or changes the model itself.
- **Cowork — sustainable** — list the lean adjustments in ≤ 4 bullets (and the
  model/effort line above if it applies), then run the leaner version on
  **go**. With a budget: shape the plan to fit it (fewer sources, shorter time
  window, fewer deliverables or iterations, no optional expensive tools) and
  pause for a check-in before any step likely to push past it (an extra
  deliverable, browser use, image generation, a long multi-file pass). Be
  honest: the budget is a target, not a hard cap — only admin spending limits
  cap spend. Suggest typing `/cost` (free) at the end to see actual usage.
- **Use M365 Copilot instead** — Read `value-and-routing.md` §4, pick the
  matching recipe (combine recipes for multi-part tasks) and give the user the
  flow: numbered steps with the app, where to click and a copy-paste prompt for
  each step, adapted to their task. Add the "stay inside your license" tip (§5).
  Then stop — do not run the task in Cowork.
- **Rescope first** — offer a tighter rewrite of their prompt (same goal, fewer
  sources / deliverables / runs) and offer to re-check it.

## Guardrails

- **Gate, not executor.** Never start the user's task, read its sources or
  create its deliverables before the user chooses in Step 6.
- **Cheap by design.** Only the lookups listed at the top; one card; at most two
  question prompts (Step 2 + Step 6), plus the "paste your task" prompt only when
  no task was given. No re-runs on follow-ups.
- **Ranges, sourced.** Every number comes from the companion files; say "rough
  estimate" when the task doesn't map cleanly. The card links to the official
  Copilot Credits Guide used for the bands.
- **Model advice is advisory.** The user picks the model and effort in the
  Cowork picker; the choice applies from their next message on. Never claim the
  skill switches models, routes steps or subagents to different models, or
  changes the model mid-run. Availability depends on the tenant — say "if it
  appears in your model picker", and recommend **Auto** when unsure.
- **Sustainability, honestly.** "Sustainable" here means the same outcome with
  fewer credits, i.e. less compute. Do not state CO₂, energy or water figures —
  no official per-task number exists.
- **No pretending to be official.** Always show the community-skill note.
  Never present the estimate as Microsoft pricing or as the bill; the real
  figure is `/cost` (free, after the fact) and the Cost Management dashboard.
- **Disclose the check's own cost.** The card's disclaimer states that this
  pre-check uses a small number of credits.

## Make it yours

Edit `pricing-reference.md` §0 (hourly rate, currency, monthly credit limit),
the model list in §4 when your picker changes, and the recipes in
`value-and-routing.md` §4 for your organization's own agents. Re-verify the
sources (dates are in each file) when Microsoft updates pricing.
